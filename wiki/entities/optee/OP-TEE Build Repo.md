---
type: entity
title: "OP-TEE Build Repo"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - build-system
  - repo-tool
status: developing
address: c-000046
related:
  - "[[OP-TEE Build System]]"
  - "[[OP-TEE Boot Flow]]"
  - "[[Trusted Firmware-A]]"
  - "[[OP-TEE OS]]"
  - "[[U-Boot]]"
  - "[[Buildroot]]"
  - "[[QEMU]]"
sources:
  - "build/ (local checkout: /home/bhaskarv/optee/build)"
---

# OP-TEE Build Repo

Upstream: `github.com/OP-TEE/build`. Not code itself: a `repo` (Android-style multi-repo tool) manifest plus a set of Makefiles that checks out and orchestrates every other OP-TEE component as one buildable system for a given target board.

## What it owns

- `.repo/manifests/*.xml`: one manifest per supported platform (`qemu_v8.xml`, `hikey.xml`, `stm32mp1.xml`, ...). Each lists the exact git repos + revisions to clone as siblings under the checkout root (this machine: `/home/bhaskarv/optee/`).
- `build/common.mk`: shared targets reused across all platforms (`buildroot`, `linux-common`, `optee-os-common`, `edk2-common`, `ftpm`, ...).
- `build/<platform>.mk` (e.g. `qemu_v8.mk`): per-target config: toolchain selection, `CFG_*` flags passed into `optee_os`, and the final `ln -sf` steps that collect built binaries into `out/bin/` as `bl1.bin`, `bl2.bin`, `bl32.bin`, `bl32_extra1.bin`, `bl32_extra2.bin`, `bl33.bin`. See [[OP-TEE Boot Flow]] for what those names mean.

## Local checkout

At `/home/bhaskarv/optee/`, siblings include `optee_os/`, `optee_client/`, `optee_test/`, `optee_examples/`, `optee_ftpm/`, `trusted-firmware-a/`, `u-boot/`, `buildroot/`, `linux/`, `qemu/`, `ms-tpm-20-ref/`, each a real upstream git clone tracking `OP-TEE/<repo>` (or the relevant third party) on GitHub: so `git log`/`git remote -v` inside any of them shows real history, not a vendored snapshot.

See [[OP-TEE Build System]] for how `make` is actually invoked here.
