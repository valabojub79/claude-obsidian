---
type: entity
title: "QEMU (OP-TEE target)"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - emulation
  - qemu-v8
status: developing
address: c-000052
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[Trusted Firmware-A]]"
  - "[[OP-TEE Build System]]"
sources:
  - "qemu/ (local checkout: /home/bhaskarv/optee/qemu)"
---

# QEMU (OP-TEE target)

The `qemu/` sibling repo is a pinned QEMU build used as the emulated hardware target for this checkout (`PLATFORM_FLAVOR=qemu_armv8a`, platform dir `optee_os/core/arch/arm/plat-vexpress/`, which forces `CFG_WITH_ARM_TRUSTED_FW=y`). It's not OP-TEE code: it's the virtual board OP-TEE runs on, standing in for real Armv8-A silicon.

## How it's started

`build/qemu_v8.mk`'s `run`/`run-only` targets launch QEMU with `-bios bl1.bin`: i.e. [[Trusted Firmware-A]]'s BL1 image is loaded directly as the platform's boot ROM/firmware image, exactly as a real board's boot ROM would jump into BL1. Everything downstream (BL2 → BL32 → BL33) proceeds the same as on real hardware. See [[OP-TEE Boot Flow]].
