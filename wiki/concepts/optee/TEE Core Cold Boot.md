---
type: concept
title: "TEE Core Cold Boot"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - boot
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000057
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[OP-TEE OS]]"
  - "[[Normal World vs Secure World]]"
sources:
  - "optee_os/core/arch/arm/kernel/entry_a64.S"
  - "optee_os/core/arch/arm/kernel/boot.c"
---

# TEE Core Cold Boot

What actually happens inside [[OP-TEE OS]] (BL32) between being handed control by BL2 and returning control to BL33: the inside of the third arrow in [[OP-TEE Boot Flow]]. Traced from `optee_os` source (arm64 path), not from docs: verify against current `master` before relying on exact function names in a patch.

## Entry

1. `_start` (`core/arch/arm/kernel/entry_a64.S:165`): the actual first instruction executed in BL32. Sets up `reset_vect_table`, copies init code/rodata, zeroes `.bss`/`.nex_bss`, sets up stacks, and (on secondary CPUs / PSCI `CPU_ON`) can instead land at `cpu_on_handler`.
2. `_start` calls into `boot_init_primary_early()` (`core/arch/arm/kernel/boot.c`), marked `__weak` so platforms can override it. Default implementation: if `CFG_TRANSFER_LIST` is set, maps and reads the TF-A transfer list (boot args handed from BL2) to locate the pageable part; otherwise falls back to `boot_arg_pageable_part`.
3. That calls `init_primary(pageable_part)`: the real core init: MMU/memory map setup, heap init, driver init, loading the pageable part (`bl32_extra2.bin`, see [[OP-TEE Boot Flow]]) via the pager if `CFG_WITH_PAGER` is set.
4. Followed by three more `__weak`, platform-overridable hooks in sequence: `boot_init_primary_late()` → `boot_init_primary_runtime()` (calls `thread_init_primary()`: sets up the per-CPU thread/stack state needed to handle SMCs) → `boot_init_primary_final()`.

## Platform specifics for this checkout

`PLATFORM_FLAVOR=qemu_armv8a` under `core/arch/arm/plat-vexpress/` (`conf.mk`), which forces `CFG_WITH_ARM_TRUSTED_FW=y`: i.e. this platform config assumes [[Trusted Firmware-A]] is present and does the BL1/BL2 work described in [[OP-TEE Boot Flow]], rather than OP-TEE's boot code doing it standalone (some non-TF-A platforms have OP-TEE do more of its own early boot).

## Return to Normal World

After `boot_init_primary_final()`, OP-TEE OS has nothing more to do on cold boot: it idles waiting for SMCs (see [[Normal World vs Secure World]]). Control passes to BL33 ([[U-Boot]]) because that's what BL2 was always going to boot next, not because OP-TEE OS explicitly "jumps" there.
