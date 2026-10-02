---
type: concept
title: "GlobalPlatform Client API Model"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - client-api
  - globalplatform
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000107
related:
  - "[[optee_client]]"
  - "[[Normal World vs Secure World]]"
  - "[[Example TA Structure]]"
  - "[[OP-TEE OS]]"
sources:
  - "optee_client/libteec/include/tee_client_api.h"
  - "optee_client/libteec/src/tee_client_api.c"
  - "optee_examples/hello_world/host/main.c"
---

# GlobalPlatform Client API Model

What a normal-world application actually calls to talk to a Trusted Application, implemented by [[optee_client]]'s `libteec` (`tee_client_api.c`). [[optee_client]] covers *why* this library exists; this page covers the shapes and call sequence.

## The call sequence

```
TEEC_InitializeContext(name, &ctx)        open a connection to the TEE
TEEC_OpenSession(&ctx, &sess, &uuid, ...)  start a session with one TA (by UUID)
TEEC_InvokeCommand(&sess, cmd_id, &op, ..) call one command in that TA, 0+ times
TEEC_CloseSession(&sess)
TEEC_FinalizeContext(&ctx)
```

Verified directly against `optee_client/libteec/src/tee_client_api.c`'s exported symbols
(`TEEC_InitializeContext`, `TEEC_OpenSession`, `TEEC_InvokeCommand`, `TEEC_CloseSession`,
`TEEC_FinalizeContext`, `TEEC_RequestCancellation`) and matched line-for-line against
`optee_examples/hello_world/host/main.c`, which runs exactly this sequence to call one TA
command.

## Key shapes (`tee_client_api.h`)

- **`TEEC_Context`**: the open connection to the TEE driver; one per process typically.
- **`TEEC_Session`**: one open session with one TA, identified by its `TEEC_UUID`.
- **`TEEC_Operation`**: the payload for one `TEEC_InvokeCommand` call. Carries
  `paramTypes` (built with the `TEEC_PARAM_TYPES()` macro) plus a 4-element
  `TEEC_Parameter params[]` array. Each parameter slot is independently typed as one of:
  - `TEEC_Value`: a small input/output/inout scalar pair (two `uint32_t`s).
  - `TEEC_TempMemoryReference`: a pointer + size, valid for the one call only.
  - `TEEC_RegisteredMemoryReference`: a reference into a `TEEC_SharedMemory` block
    that's been explicitly registered/allocated up front and can be reused across calls.
- **`TEEC_SharedMemory`**: a memory block shared with the TEE, created via
  `TEEC_RegisterSharedMemory()` (wrap already-allocated host memory) or
  `TEEC_AllocateSharedMemory()` (let the API allocate it), released with
  `TEEC_ReleaseSharedMemory()`.

## Why the distinction matters

Temp memory references are simpler but get copied per call; registered shared memory
avoids that copy for data reused across many `TEEC_InvokeCommand` calls (e.g. a large
buffer in a crypto or storage example). A TA implementation reviewed for performance
should be checked against which of these it actually needs, not just whether it works.

## TA side of the same call

On the other end of `TEEC_OpenSession`/`TEEC_InvokeCommand`, the matching entry points
run inside the TA in secure world (`TA_OpenSessionEntryPoint`,
`TA_InvokeCommandEntryPoint`): see [[Example TA Structure]]. The world switch itself
(how an `TEEC_InvokeCommand` call turns into an SMC and back) is [[Normal World vs Secure World]]'s territory.
