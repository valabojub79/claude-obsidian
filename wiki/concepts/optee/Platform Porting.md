---
type: concept
title: "Platform Porting"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - porting
  - platform
complexity: advanced
domain: trusted-execution
status: developing
address: c-000121
related:
  - "[[QEMU]]"
  - "[[OP-TEE OS]]"
  - "[[Secure Boot Chain of Trust]]"
  - "[[Device Tree in OP-TEE]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_os/core/arch/arm/plat-vexpress/"
  - "https://optee.readthedocs.io/en/latest/architecture/porting_guidelines.html"
---

# Platform Porting

What a new `plat-<name>/` port actually needs, beyond what the `optee-feature-design`
Claude Code skill already states (that skill covers *where* platform code lives in the
tree; this page covers *what has to be real* for the port to be production-grade
rather than a QEMU-style development stub). [[QEMU]]'s own platform,
`core/arch/arm/plat-vexpress/`, is a working example of the file layout, but it is
itself a development target, so several of the items below are deliberately stubbed
there and must NOT be copied as-is into a real product port.

## The three files every port needs (confirmed layout)

`core/arch/arm/plat-vexpress/` contains exactly this set: `conf.mk`, `main.c`,
`platform_config.h`, `sub.mk`, plus board-specific files (here,
`juno_core_pos_a{32,64}.S`). Per the upstream porting guide:
- **`conf.mk`**: `CFG_*` build flags, compiler flags, core count/architecture.
- **`main.c`**: SMC thread handlers, FIQ handling, UART console init.
- **`platform_config.h`**: the memory map: TZSRAM, TZDRAM, TEE RAM, TA RAM, shared
  memory addresses/sizes.

## Things that are stubbed on QEMU and must be real on actual hardware

These are the items the upstream porting guide calls out explicitly as needing a real
implementation on a shipping device: treat this as the pre-upstream checklist for a
platform port, not just a style issue:

- **Hardware Unique Key (HUK)**: `tee_otp_get_hw_unique_key()` returns zeros by
  default ("just stubbed"). A real port needs a crypto accelerator or secure
  co-processor backing this: never ship with a zeroed/software-only HUK.
- **Secure time**: `tee_time_get_sys_time()` (system time) and
  `tee_time_get_ta_time()` (TA persistent time) per the GlobalPlatform spec. If the
  SoC has a secure RTC, wire it in here instead of trusting normal-world time.
- **RNG / entropy**: default is a software PRNG with weak entropy
  (`CFG_WITH_SOFTWARE_PRNG=y`). Production: set `CFG_WITH_SOFTWARE_PRNG=n` and
  implement `hw_get_random_bytes()` against real hardware entropy; optionally expose
  it to the normal world via `CFG_HWRNG_PTA`.
- **PSCI power management**: `cpu_off`, `cpu_suspend`, `cpu_resume`, `system_off`,
  `system_reset` start as stubs. A real port needs these to actually save/restore
  secure hardware IP state and re-arm memory firewalls across power transitions.
- **Memory firewall (TZASC or equivalent)**: the SoC's secure/non-secure memory
  partitioning must actually be configured: this is a hardware-specific step with no
  generic OP-TEE code to fall back on.
- **Root of trust**: a real chain of trust needs public-key hashes burned into OTP and
  checked against bootloader signatures. On Armv8-A, this is normally delegated to
  [[Trusted Firmware-A]]'s Trusted Board Boot (see [[Secure Boot Chain of Trust]])
  rather than reimplemented in `optee_os` itself.
- **TA signing key**: `keys/default_ta.pem` is a published development key: "never
  ever check in this private key" for a real product. Use an HSM-managed production
  key instead.

## Optional but expected for a serious port

- **Crypto acceleration**: register hardware crypto support through the `drvcrypt`
  framework's `drvcrypt_register_*()` API rather than falling back to the software
  `libtomcrypt`/`libmbedtls` paths for everything.
- **Device tree wiring**: see [[Device Tree in OP-TEE]] for how the platform's memory
  map and OP-TEE's own config interact with DT at boot.

## Getting it merged upstream (not just working)

The porting guide is explicit that upstreaming a new board, beyond the code itself,
expects: platform documentation added, the device wired into CI (`.shippable.yml`),
and a maintainer who commits to periodic (quarterly) testing of the platform: an
unmaintained platform port is a liability the project doesn't want merged. Cross-check
code style against [[OP-TEE Coding Standards]] before opening the PR; see the
`optee-contribution-workflow` skill for the submission mechanics.
