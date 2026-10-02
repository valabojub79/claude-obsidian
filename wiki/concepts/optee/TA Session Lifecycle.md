---
type: concept
title: "TA Session Lifecycle"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - trusted-applications
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000078
related:
  - "[[Pseudo-TA vs User-Mode TA]]"
  - "[[ldelf TA Loader]]"
  - "[[Normal World vs Secure World]]"
  - "[[optee_client]]"
sources:
  - "optee_os/core/kernel/tee_ta_manager.c"
  - "optee_os/core/kernel/user_ta.c"
---

# TA Session Lifecycle

The secure-world-side dispatch for the GP open-session / invoke-command /
close-session cycle: what happens inside [[OP-TEE OS]] after
[[Normal World vs Secure World]]'s SMC has already landed and been routed to the
right TA. Client-side (`optee_client`'s `libteec`) lifecycle calls are the normal-world
mirror of this; this page covers the secure-world receiving end.

## The three core entry points

`core/kernel/tee_ta_manager.c` owns session management for *any* TA context
(pseudo or user-mode):

- `tee_ta_open_session()`: resolves the target UUID to a TA context (loading it via
  [[ldelf TA Loader]] if it's a user-mode TA not already resident, or looking up the
  statically-registered pseudo-TA: see [[Pseudo-TA vs User-Mode TA]]), creates a
  session, and calls through to the TA's `open_session_entry_point`.
- `tee_ta_invoke_command()`: looks up an existing session by ID and dispatches a
  command ID + parameters to the TA's `invoke_command_entry_point`.
- Session close goes through the matching close path, tearing the session down and,
  if the TA isn't `TA_FLAG_INSTANCE_KEEP_ALIVE` and has no other open sessions,
  potentially unloading the instance entirely.

## How a user-mode TA actually gets entered (the privilege switch)

For a user-mode TA, `tee_ta_manager.c` doesn't call the TA's code directly: it can't,
the TA runs unprivileged. `core/kernel/user_ta.c` is the layer that performs the
switch. Three thin wrappers (`user_ta_enter_open_session()`,
`user_ta_enter_invoke_cmd()`, `user_ta_enter_close_session()`) all funnel into one
function, `user_ta_enter()`, which:

1. Maps the caller's parameters into the TA's address space (`vm_map_param()`).
2. Builds a `struct utee_params` on the TA's user-mode stack.
3. Calls `thread_enter_user_mode(func, ...)`: **this is the actual S-EL1→S-EL0
   privilege-level switch**, jumping to `utc->uctx.entry_func` (the real TA entry
   point [[ldelf TA Loader]] resolved) with `func` telling the TA-side dispatch stub
   which GP lifecycle call this is (open session / invoke command / close session /
   etc.: an `enum utee_entry_func`).
4. On return, checks `utc->ta_ctx.panicked`: a TA crash here becomes
   `TEE_ERROR_TARGET_DEAD` back up the call chain, not a kernel panic; `OP-TEE OS`
   itself survives a crashing TA, which is the entire point of the isolation
   described in [[Pseudo-TA vs User-Mode TA]].
5. Copies result values back out of the shared `utee_params` buffer
   (`update_from_utee_param()`).

A pseudo-TA skips `user_ta_enter()`/`thread_enter_user_mode()` entirely: its
`open_session_entry_point`/`invoke_command_entry_point` are plain function pointers
in core, called directly at S-EL1: consistent with it having no isolation boundary
from core in the first place.

## Recursion guard

`user_ta_enter()` tracks recursion depth per-thread (`inc_recursion()`/
`dec_recursion()`, capped at `CFG_CORE_MAX_SYSCALL_RECURSION`): relevant because a TA
can itself open a session to *another* TA mid-command, which re-enters this same path.
