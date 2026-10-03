---
type: concept
title: "Thread Model and RPC"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - thread-model
  - smc
  - rpc
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000062
related:
  - "[[Normal World vs Secure World]]"
  - "[[Shared Memory Model]]"
  - "[[OP-TEE OS]]"
  - "[[optee_client]]"
sources:
  - "optee_os/core/arch/arm/kernel/thread.c"
  - "optee_os/core/arch/arm/kernel/thread_optee_smc.c"
  - "optee_os/core/include/kernel/thread.h"
---

# Thread Model and RPC

[[Normal World vs Secure World]] covers the SMC world-switch at a high level. This
page goes one level deeper: how OP-TEE OS actually schedules work across SMC calls,
and how a TA can ask normal world to do something on its behalf mid-call (RPC).

## Threads are per-SMC-call contexts, not OS threads

OP-TEE OS has a fixed pool of "threads" (`CFG_NUM_THREADS`), each a secure-world
execution context (own stack, saved registers) bound to one normal-world call at a
time. This is not preemptive multitasking: a thread runs until the TA call completes
or it needs to RPC out to normal world.

- `thread_alloc_and_run()` (via the static `__thread_alloc_and_run()`): picks a free
  thread slot and starts running the requested secure-world entry point for an
  incoming SMC.
- `thread_state_free()`: releases a thread slot back to the pool when a call fully
  completes.
- `thread_resume_from_rpc(thread_id, a0, a1, ...)`: resumes a thread that was
  suspended mid-call waiting on an RPC response from normal world.

## How an RPC round-trip works

A TA (or OP-TEE OS core code acting on its behalf) sometimes needs normal world to do
something it has no secure-world equivalent for: read a file, get wall-clock time,
allocate shared memory. The mechanism:

1. Secure-world code calls `__thread_rpc(rv[THREAD_RPC_NUM_ARGS])` (in `thread.c`).
   This doesn't return to the TA: it returns *out* through the original SMC, back to
   the normal-world caller, carrying an `OPTEE_SMC_RETURN_RPC`-class return code and
   an RPC command.
2. Normal world (via [[optee_client]]'s driver/`libteec`/`tee-supplicant` stack)
   sees the RPC return code, services the request, and issues a *new* SMC carrying
   the result plus the same `thread_id`.
3. OP-TEE OS's `thread_resume_from_rpc()` matches that `thread_id` back to the
   suspended secure-world context and resumes it exactly where `__thread_rpc()` left
   off, with the result now available.

The RPC command codes are real, defined in `core/include/optee_rpc_cmd.h`
(`OPTEE_RPC_CMD_*`): `LOAD_TA` (0), `RPMB` (1), `FS` (2, normal-world-backed secure
storage I/O), `GET_TIME` (3), `NOTIFICATION` (4), `SUSPEND` (5), `SHM_ALLOC` (6) /
`SHM_FREE` (7), `SOCKET` (10), `SUPP_PLUGIN` (12), among others. `FS` is the concrete
case that makes REE-filesystem-backed secure storage possible at all: OP-TEE OS has
no filesystem of its own, so a TA's storage read/write becomes an `OPTEE_RPC_CMD_FS`
RPC serviced by `tee-supplicant` in normal-world Linux.

## Where payload memory for an RPC comes from

`thread_rpc_alloc_payload(size)` (`thread_optee_smc.c`) allocates the shared-memory
buffer used to carry RPC request/response data across the world switch. See
[[Shared Memory Model]] for how that memory is actually represented (`mobj`) and how
it differs from memory a TA registers itself.
