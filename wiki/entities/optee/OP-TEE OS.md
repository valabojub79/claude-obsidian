---
type: entity
title: "OP-TEE OS"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - trusted-execution
  - tee-kernel
status: developing
address: c-000048
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[TEE Core Cold Boot]]"
  - "[[Normal World vs Secure World]]"
  - "[[OP-TEE Coding Standards]]"
  - "[[optee_client]]"
  - "[[Trusted Firmware-A]]"
sources:
  - "optee_os/ (local checkout: /home/bhaskarv/optee/optee_os)"
---

# OP-TEE OS

Upstream: `github.com/OP-TEE/optee_os`. The TEE itself: this *is* OP-TEE. Runs in ARM TrustZone secure world (S-EL1), implements the GlobalPlatform TEE Internal Core API for Trusted Applications, and is the thing [[Trusted Firmware-A]] loads as **BL32**.

## Directory layout (`optee_os/`)

- `core/`: the TEE kernel: `core/arch/` (per-architecture entry/boot/MMU/thread code: see [[TEE Core Cold Boot]]), `core/kernel/`, `core/crypto/`, `core/drivers/`, `core/mm/` (memory management/pager), `core/pta/` (pseudo Trusted Applications), `core/tee/` (syscall dispatch to user-mode TAs).
- `ldelf/`: the tiny secure-world loader that maps and starts user-mode TA ELF binaries.
- `lib/`: `libutee` (TA-side GP API), `libutils`, `libmbedtls`, etc. (see [[TA Library Stack]] for the full breakdown).
- `ta/`: example/reference Trusted Applications.
- `mk/`: shared Make fragments (`compile.mk`, `config.mk`, `lib.mk`, ...) included by `core.mk` / `crypto.mk`.

## Build output

For the `qemu_v8` target, `make` produces three separate images under `optee_os/out/arm/core/`: `tee-header_v2.bin`, `tee-pager_v2.bin`, `tee-pageable_v2.bin`. `build/qemu_v8.mk` symlinks these into `out/bin/` as `bl32.bin`, `bl32_extra1.bin`, `bl32_extra2.bin` respectively: the split exists because of the demand-paging design (see [[OP-TEE Boot Flow]]).

Coding rules for contributing here: [[OP-TEE Coding Standards]].
