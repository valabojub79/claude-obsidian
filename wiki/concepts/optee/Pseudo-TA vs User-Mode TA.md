---
type: concept
title: "Pseudo-TA vs User-Mode TA"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - trusted-applications
  - hub
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000075
related:
  - "[[OP-TEE OS]]"
  - "[[Normal World vs Secure World]]"
  - "[[TA Session Lifecycle]]"
  - "[[TA Properties and Manifest]]"
  - "[[ldelf TA Loader]]"
  - "[[TA Storage and Loading]]"
sources:
  - "optee_os/core/include/kernel/pseudo_ta.h"
  - "optee_os/core/pta/device.c"
  - "https://optee.readthedocs.io/en/latest/architecture/trusted_applications.html"
---

# Pseudo-TA vs User-Mode TA

**Hub page** for the Trusted Applications domain. OP-TEE has two completely different
ways to add a service that runs inside [[OP-TEE OS]], with a real trust boundary
between them.

## The distinction

| | Pseudo-TA | User-mode TA |
|---|---|---|
| Lives where | Statically linked into the core blob, `optee_os/core/pta/` | A separate ELF binary, loaded at runtime |
| Privilege level | **Same** privilege level as OP-TEE core itself (S-EL1) | Unprivileged, S-EL0 (lower than core) |
| Isolation from core | None: a bug in a pseudo-TA can corrupt core state | Real: a crashing/malicious TA can't take down core |
| API available | OP-TEE core-internal APIs/routines only, no GP API | Full GlobalPlatform TEE Internal Core API via `libutee` |
| How it's invoked | Same session/command dispatch as a user-mode TA (see [[TA Session Lifecycle]]), but the entry points run in-core | Loaded by [[ldelf TA Loader]], entered via a privilege-level switch |

The upstream docs are blunt about which to prefer: *"In most cases an unprivileged
(user mode) TA is the best choice instead of adding your code directly to the OP-TEE
core."* Pseudo-TAs exist for a narrow set of cases: privileged operations that
genuinely need direct core access (e.g. [[OP-TEE OS]]'s own test/stats/attestation
PTAs in `core/pta/`), not as the default way to add a feature. See
`optee-feature-design` (project skill) before picking one.

## Registration (pseudo-TA)

A pseudo-TA registers itself with a `pseudo_ta_register(...)` macro
(`core/include/kernel/pseudo_ta.h`), filling a `struct pseudo_ta_head`: UUID, name,
flags, and the four GP-style entry points (`create_entry_point`,
`open_session_entry_point`, `invoke_command_entry_point`,
`close_session_entry_point`). Real example, `core/pta/device.c`:

```c
pseudo_ta_register(.uuid = PTA_DEVICE_UUID, .name = PTA_NAME,
		   .flags = PTA_DEFAULT_FLAGS,
		   .invoke_command_entry_point = invoke_command);
```

Allowed flags for a pseudo-TA are deliberately restricted
(`PTA_MANDATORY_FLAGS`/`PTA_ALLOWED_FLAGS` in `pseudo_ta.h`): always single-instance,
multi-session, keep-alive, plus optionally `TA_FLAG_SECURE_DATA_PATH`,
`TA_FLAG_CONCURRENT`, `TA_FLAG_DEVICE_ENUM`: a pseudo-TA can't opt out of the
always-resident, shared-instance model the way a user-mode TA can (see
[[TA Properties and Manifest]]).

## Where user-mode TAs differ structurally

A user-mode TA is a real ELF binary with its own `struct ta_head` (UUID, stack size,
flags) and links against `lib/libutee`, which mediates every GP API call through a
syscall into [[OP-TEE OS]] rather than calling core functions directly. How that
binary actually gets mapped and started is [[ldelf TA Loader]]; where it physically
comes from (built into the core blob, the REE filesystem, or encrypted secure
storage) is [[TA Storage and Loading]].
