---
type: concept
title: "ldelf TA Loader"
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
address: c-000076
related:
  - "[[Pseudo-TA vs User-Mode TA]]"
  - "[[OP-TEE OS]]"
  - "[[TA Session Lifecycle]]"
  - "[[TA Storage and Loading]]"
  - "[[Normal World vs Secure World]]"
sources:
  - "optee_os/ldelf/main.c"
  - "optee_os/core/kernel/ldelf_loader.c"
  - "https://optee.readthedocs.io/en/latest/architecture/trusted_applications.html"
---

# ldelf TA Loader

How a user-mode TA's ELF binary actually gets mapped into memory and started at
S-EL0, regardless of whether it came from the core blob, the REE filesystem, or
secure storage (see [[TA Storage and Loading]] for where the bytes come from before
this point). Traced from `optee_os` source; verify against current `master` before
relying on exact function names in a patch.

## ldelf is itself a loaded ELF binary

`ldelf` is not part of [[OP-TEE OS]] core: it's a small unprivileged ELF program that
core loads first, then uses as a bootstrap loader for the real TA. The kernel-side
driver of this two-stage load lives in `core/kernel/ldelf_loader.c`:

1. `ldelf_load_ldelf(uctx)`: maps the `ldelf` binary itself into the TA's new address
   space and sets `uctx->entry_func = code_addr + ldelf_entry` (ldelf's own entry
   point, not the TA's yet).
2. `ldelf_init_with_ldelf(sess, uctx)`: performs a privilege-level switch into that
   entry point (the actual S-EL1→S-EL0 transition happens via `thread_enter_user_mode`,
   see [[TA Session Lifecycle]]), running `ldelf()` in `ldelf/main.c`.

## What `ldelf()` does once running

Inside `ldelf/main.c`, the `ldelf()` function (given an `ldelf_arg` with the target
TA's UUID):

1. `ta_elf_load_main(&arg->uuid, ...)`: loads the main TA ELF and builds a list of
   its dependencies (shared libraries the TA links against).
2. Loops `ta_elf_load_dependency()` over the dependency list: this loop can grow the
   list as dependencies pull in further dependencies, so it runs until nothing new
   is added.
3. For every loaded ELF: `ta_elf_relocate()` then `ta_elf_finalize_mappings()`:
   standard ELF relocation and finalizing the memory mappings/permissions.
4. `ta_elf_finalize_load_main(&arg->entry_func, &arg->load_addr)`: this is the
   payoff: it writes the **real TA's** entry point and load address into
   `arg->entry_func`/`arg->load_addr`.
5. Sets up `arg->dl_entry` (for `dlopen()`/`dlsym()` support after the TA is running)
   and, if tracing is enabled, `arg->ftrace_entry` / `arg->dump_entry` (used if the TA
   crashes, to print a stack trace via `dump_ta_state()`).
6. Returns via `sys_return_cleanup()`: a syscall back into core, not a normal
   function return, since `ldelf` is running unprivileged.

Back in `core/kernel/ldelf_loader.c`, `ldelf_init_with_ldelf()` picks up that returned
`arg_bbuf` and **overwrites** `uctx->entry_func` with the real TA's entry point
(`arg_bbuf->entry_func`): this is the moment control conceptually transfers from
"loading ldelf" to "ready to run the actual TA." The next privilege-level switch into
`uctx->entry_func` enters the TA itself, invoking whichever GP entry point the session
lifecycle calls first (see [[TA Session Lifecycle]]).

## ldelf stays resident

Unlike a loader that exits after loading, `ldelf` keeps running in the TA's address
space afterward. This is why `uctx->dl_entry_func`/`dump_entry_func`/`ftrace_entry_func`
get wired up: dynamic linking (`dlopen`/`dlsym`) and post-crash stack traces both need
`ldelf` to still be there to service them (`ldelf_dlopen()`, `ldelf_dlsym()`,
`ldelf_dump_state()`, `ldelf_dump_ftrace()` in `ldelf_loader.c` each re-enter `ldelf`
through the same `thread_enter_user_mode()` mechanism, just at different entry points
within it).
