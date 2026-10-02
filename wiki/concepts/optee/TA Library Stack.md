---
type: concept
title: "TA Library Stack"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - libraries
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000109
related:
  - "[[OP-TEE OS]]"
  - "[[Example TA Structure]]"
  - "[[TEE Core Cold Boot]]"
sources:
  - "https://optee.readthedocs.io/en/latest/architecture/libraries.html"
  - "optee_os/lib/"
---

# TA Library Stack

What a Trusted Application is actually linked against, below the GP TEE Internal Core
API it calls directly. Confirmed against both `optee_os/lib/`'s real directory listing
and the upstream architecture doc: they agree.

## The five libraries (`optee_os/lib/`)

| Library | Provides | Notes |
|---|---|---|
| `libutee` | The GP **TEE Internal Core API** itself. Some calls are implemented directly in the library; others are thin wrappers that make a syscall into [[OP-TEE OS]] core. | Always linked. UUID when loaded as a shared library: `4b3d937e-d57e-418b-8673-1c04f2420226`. |
| `libutils` | A standard C library subset for TAs (`snprintf`, `strncmp`, `memcpy`, `malloc`, `qsort`, ...), not the full libc surface. | Prefer the equivalent GP API call over the libc one where both exist, for portability across GP-compliant TEE implementations, not just OP-TEE. UUID: `71855bba-6055-4293-a63f-b0963a737360`. |
| `libmbedtls` | Mbed TLS, for TAs that need crypto operations beyond what the GP Crypto API already covers, or that need Mbed TLS's specific API surface. | Needs matching build flags to also be embedded in OP-TEE core. UUID: `87bb6ae8-4b1d-49fe-9986-2b966132c309`. |
| `libunw` | Stack unwinding / backtrace support, used by both TAs and OP-TEE core itself. | Always linked statically (no shared-library UUID). |
| `libdl` | `dlopen()`/`dlsym()`/`dlclose()` for TAs that load other shared libraries at runtime. | UUID: `be807bbd-81e1-4dc4-bd99-3d363f240ece`. Exercised by `optee_test/ta/os_test_lib_dl`. |

## Static vs. shared

Each of these (except `libunw`) has a UUID "when shared": OP-TEE supports loading a
library as a separate shared-library TA-like image at runtime (loaded once, used by
multiple TAs) as an alternative to statically linking a private copy into every TA
binary. Which mode is in play is a build-time choice per library/TA, not a fixed
architecture decision: check the specific `conf.mk`/`sub.mk` flags for a given build
rather than assuming either mode.

## Where this sits in the TA's actual execution

[[ldelf TA Loader|ldelf]] (OP-TEE OS's secure-world ELF loader, see [[OP-TEE OS]]) is what actually maps
a TA's ELF binary and its linked libraries into memory and starts it: this library
stack is what that loaded binary is linked against, not something ldelf itself provides.
