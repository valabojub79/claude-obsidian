---
type: concept
title: "OP-TEE Build System"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - build-system
  - make
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000054
related:
  - "[[OP-TEE Build Repo]]"
  - "[[OP-TEE Boot Flow]]"
  - "[[Buildroot]]"
sources:
  - "build/common.mk"
  - "build/qemu_v8.mk"
---

# OP-TEE Build System

How the [[OP-TEE Build Repo]] turns ~10 independent git repos into one bootable image.

## Structure

- `build/common.mk`: platform-agnostic targets shared by every board: `buildroot`, `linux-common`, `optee-os-common`, `optee-os-devkit`, `edk2-common`, `ftpm`, etc. Each wraps a `$(MAKE) -C <repo> O=<out-dir> ...` invocation with the right cross-compiler and flags.
- `build/<platform>.mk` (e.g. `qemu_v8.mk`, `hikey.mk`, `stm32mp1.mk`): included on top of `common.mk`; sets `PLATFORM`, toolchain paths, `CFG_*` config passed into `optee_os`'s Kconfig-like build, and defines the final `all` target plus `run`/`run-only` (QEMU launch) and image-assembly (`ln -sf` into `out/bin/`) steps.
- `toolchains/`: cross-compiler toolchains downloaded/unpacked per architecture, referenced by the platform `.mk` files.

A top-level `make` in `build/` therefore fans out into: toolchain setup → `trusted-firmware-a` → `optee_os` → `u-boot` → `buildroot` (+ `optee_client`/`optee_test` built *into* the buildroot rootfs) → final symlink/image assembly. See [[OP-TEE Boot Flow]] for what the resulting images are and how they chain at runtime.

## Known build gotcha (this environment)

Buildroot's `support/dependencies/dependencies.mk` hard-fails with *"Your PATH contains spaces, TABs, and/or newline characters"* if `PATH` has any whitespace-containing entries. On WSL, Windows' `PATH` is auto-imported and typically includes space-containing entries like `/mnt/c/Program Files/...`: those must be stripped from `PATH` before running `make` here. (Fixed in this environment via a `~/.bashrc` filter.)
