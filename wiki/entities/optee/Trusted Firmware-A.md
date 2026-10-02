---
type: entity
title: "Trusted Firmware-A"
created: 2026-10-02
updated: 2026-10-02
tags:
  - entity
  - optee
  - trusted-execution
  - firmware
  - arm
status: developing
address: c-000047
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[Secure Boot Chain of Trust]]"
  - "[[OP-TEE OS]]"
  - "[[U-Boot]]"
sources:
  - "trusted-firmware-a/ (local checkout: /home/bhaskarv/optee/trusted-firmware-a)"
---

# Trusted Firmware-A (TF-A)

Upstream: `github.com/TF-A/trusted-firmware-a`. ARM's reference secure-world boot firmware for Armv8-A. Independent project from OP-TEE, but OP-TEE's QEMU/most-Armv8 targets rely on it for the earliest boot stages and the EL3 runtime.

## Role in this checkout

Provides **BL1** and **BL2** (and, on some platforms, **BL31**, the EL3 runtime/PSCI monitor). For the `qemu_v8` target used in this checkout, QEMU is launched directly with `-bios bl1.bin`: TF-A's BL1 is the very first code executed. BL1 then loads and authenticates BL2, which in turn loads and authenticates the next-stage images: OP-TEE OS (BL32) and U-Boot (BL33). See [[OP-TEE Boot Flow]] for the full chain and [[Secure Boot Chain of Trust]] for the authentication side.

## Build artifacts (qemu_v8, release)

Built under `trusted-firmware-a/build/qemu/release/`: `bl1.bin`, `bl2.bin`, plus (for Trusted Board Boot / SPMC configurations) `*.crt` certificates and `fdts/*.dtb`. `build/qemu_v8.mk` symlinks these into `out/bin/`.
