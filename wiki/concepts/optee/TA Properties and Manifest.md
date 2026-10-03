---
type: concept
title: "TA Properties and Manifest"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - trusted-applications
complexity: beginner
domain: trusted-execution
status: developing
address: c-000077
related:
  - "[[Pseudo-TA vs User-Mode TA]]"
  - "[[ldelf TA Loader]]"
  - "[[TA Storage and Loading]]"
sources:
  - "optee_os/lib/libutee/include/user_ta_header.h"
  - "optee_os/ta/avb/user_ta_header_defines.h"
  - "https://optee.readthedocs.io/en/latest/architecture/trusted_applications.html"
---

# TA Properties and Manifest

How a user-mode TA declares what it needs and how it should be run, before any of
[[ldelf TA Loader]]'s loading logic even starts. All of this is macros in a
`user_ta_header_defines.h` the TA author writes, consumed to build a `struct ta_head`
that ends up embedded in the TA's ELF.

## The real struct (not just docs)

`lib/libutee/include/user_ta_header.h` defines what actually gets embedded:

```c
struct ta_head {
	TEE_UUID uuid;
	uint32_t stack_size;
	uint32_t flags;
	uint64_t depr_entry;
};
```

A concrete example, `ta/avb/user_ta_header_defines.h` (the Android Verified Boot TA):

```c
#define TA_UUID        TA_AVB_UUID
#define TA_FLAGS       (TA_FLAG_SINGLE_INSTANCE | TA_FLAG_MULTI_SESSION)
#define TA_STACK_SIZE  (16 * 1024)
#define TA_DATA_SIZE   (16 * 1024)
#define TA_VERSION     "1.0"
#define TA_DESCRIPTION "Android Verfied Boot"
```

## What each property actually controls

- **`TA_UUID`**: not really a "property," an identifier. REE-filesystem TAs are named
  `<uuid>.ta`; secure-storage TAs are indexed by UUID in an encrypted `dirf.db` (see
  [[TA Storage and Loading]]).
- **`TA_FLAG_SINGLE_INSTANCE`**: one instance serves every session if set; unset means
  a fresh instance per `open session` call.
- **`TA_FLAG_MULTI_SESSION`**: only meaningful if single-instance is set. With it, one
  instance handles multiple concurrent sessions; without it, a second concurrent
  `open session` gets a busy error.
- **`TA_FLAG_INSTANCE_KEEP_ALIVE`**: only meaningful if single-instance is set. The
  instance survives after its last session closes, persisting until TEE reboot.
- **`TA_STACK_SIZE` / `TA_DATA_SIZE`**: stack size and heap pool size (for
  `TEE_Malloc()`), in bytes: both mandatory, no defaults.
- **`TA_VERSION` / `TA_DESCRIPTION`**: free-form strings, default to "Undefined
  version"/"Undefined description" if omitted. No parsed format: purely metadata.
- **`TA_FLAG_SECURE_DATA_PATH`**: declares the TA can accept secure-data-path memory
  reference parameters. Omit it and the TA can't handle SDP buffers at all.
- **`TA_FLAG_CACHE_MAINTENANCE`**: gates access to the cache-maintenance syscall
  extension.
- **`TA_FLAG_CONCURRENT`**: pseudo-TA-only (see [[Pseudo-TA vs User-Mode TA]]): lets
  one PTA instance execute multiple sessions truly concurrently, not just
  multi-session.
- **`TA_FLAG_DEVICE_ENUM*`** (`_SUPP`, `_TEE_STORAGE_PRIVATE`): control *when* in the
  boot sequence the TA gets enumerated to the normal world (before/after
  `tee-supplicant` and secure storage come up): relevant for early TAs, see
  [[TA Storage and Loading]].
- **`gpd.ta.endian`**: a GP standard property OP-TEE pins to little-endian (0) only;
  big-endian TAs aren't supported.

All flags are OR'd into `TA_FLAGS`, masked by `TA_FLAGS_MASK` in
`user_ta_header.h`: a flag bit outside that mask is a build-time error, not a
silently-ignored typo.
