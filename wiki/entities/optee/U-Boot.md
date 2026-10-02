---
type: entity
title: "U-Boot"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - bootloader
status: developing
address: c-000049
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[Normal World vs Secure World]]"
  - "[[Buildroot]]"
sources:
  - "u-boot/ (local checkout: /home/bhaskarv/optee/u-boot)"
---

# U-Boot

Upstream: `github.com/u-boot/u-boot` (mirrored/pinned by the [[OP-TEE Build Repo]] manifest). The normal-world bootloader: this is **BL33** in the boot chain. Runs in Normal World at EL1/EL2, after [[Trusted Firmware-A]]'s BL2 hands control to it (having already started OP-TEE OS as BL32 first). Its job is to then load and boot the Linux kernel + the [[Buildroot]]-built root filesystem.

## Build artifact

`u-boot/u-boot.bin`, symlinked by `build/qemu_v8.mk` into `out/bin/bl33.bin`.
