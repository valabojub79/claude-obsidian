---
type: concept
title: "Shared Memory Model"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - shared-memory
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000063
related:
  - "[[Thread Model and RPC]]"
  - "[[Memory Management]]"
  - "[[Normal World vs Secure World]]"
  - "[[optee_client]]"
sources:
  - "optee_os/core/arch/arm/kernel/thread_optee_smc.c"
  - "optee_os/core/tee/entry_std.c"
---

# Shared Memory Model

How normal-world memory becomes visible to secure world, and vice versa. Distinct
from [[Memory Management]]'s `tee_mm`/`core_mmu` (which manage memory secure world
owns outright): shared memory is normal-world-owned memory that secure world maps
temporarily, tracked through an object called an `mobj`.

## mobj: the handle for "memory, wherever it actually lives"

`struct mobj` is OP-TEE OS's abstraction for a memory object regardless of backing:
secure RAM, paged memory, or normal-world shared memory all get represented as some
`mobj` subtype, so the rest of the core (TA parameter passing, the pager, RPC
payloads) can treat them uniformly. The functions relevant to shared memory
specifically:

- `mobj_mapped_shm_alloc(&pa, 1, 0, cookie)` (`thread_optee_smc.c`): wraps a chunk of
  normal-world physical memory, identified by a client-supplied `cookie`, as an
  `mobj` secure world can map and use.
- `mobj_reg_shm_get_by_cookie(cookie)`: looks up an already-registered shared-memory
  `mobj` by its cookie, rather than creating a new mapping each time.
- `mobj_reg_shm_unguard()` / `mobj_reg_shm_release_by_cookie()`
  (`core/tee/entry_std.c`'s `register_shm()`/`unregister_shm()`): explicit
  registration and release of normal-world memory, driven by `OPTEE_MSG_CMD_*`
  messages a client sends before/after using a shared buffer across several calls.

## Two ways shared memory gets used

1. **Client-registered SHM**: [[optee_client]]'s `libteec` (GlobalPlatform
   `TEEC_RegisterSharedMemory` / `TEEC_AllocateSharedMemory`) registers a normal-world
   buffer up front; `register_shm()`/`unregister_shm()` in `entry_std.c` handle the
   secure-world side of that registration, keyed by a cookie the client controls.
2. **RPC payload SHM**: when secure world itself needs a buffer to hand data back to
   normal world mid-call (see [[Thread Model and RPC]]), it goes the other direction:
   `thread_rpc_alloc_payload()` asks normal world (via an `OPTEE_RPC_CMD_SHM_ALLOC`
   RPC) to hand back memory, which secure world then wraps as an `mobj` the same way.

## Why this separation matters

Secure world never blindly trusts a physical address a client claims is shared
memory: every access goes through the `mobj` layer, which is what lets OP-TEE OS
verify (via `core_mmu`'s static map, see [[Memory Management]]) that a claimed
address actually falls in a normal-world-accessible region before mapping it into
secure address space. This is the boundary that keeps a malicious or buggy
normal-world client from tricking secure world into mapping secure-only memory as if
it were shared.
