---
type: concept
title: "Hardening: ASLR and Stack Canaries"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - hardening
  - security
complexity: advanced
domain: trusted-execution
status: developing
address: c-000122
related:
  - "[[OP-TEE OS]]"
  - "[[TEE Core Cold Boot]]"
  - "[[OP-TEE Coding Standards]]"
sources:
  - "optee_os/core/arch/arm/arm.mk"
  - "optee_os/mk/config.mk"
  - "optee_os/core/arch/arm/kernel/boot.c"
  - "https://optee.readthedocs.io/en/latest/architecture/aslr.html"
  - "https://optee.readthedocs.io/en/latest/architecture/stack_canaries.html"
---

# Hardening: ASLR and Stack Canaries

Two independent compile-time hardening mechanisms in [[OP-TEE OS]], confirmed against
`core/arch/arm/arm.mk`, `mk/config.mk`, and `core/arch/arm/kernel/boot.c`.

## ASLR: two separate knobs, not one

- **`CFG_CORE_ASLR`**: randomizes the virtual address OP-TEE core itself is mapped at.
  The core is built as position-independent code with runtime relocations applied
  during early boot, before the MMU is fully set up: `core/arch/arm/kernel/boot.c`
  guards this logic behind `#ifdef CFG_CORE_ASLR` in several places (lines ~438, 465,
  1053, 1242-1290), and comments there note: *"With CFG_CORE_ASLR=y the init part is
  relocated very early during boot... If CFG_CORE_ASLR=n, nothing needs to be done."*
  `core/arch/arm/arm.mk:284` ties this to `CFG_CORE_PHYS_RELOCATABLE` as an
  either/or pair (`cfg-one-enabled`).
- **`CFG_TA_ASLR`**: randomizes where a user-mode Trusted Application loads, completely
  independent of core ASLR. Pseudo-TAs are excluded, since they're compiled into the
  core image itself and don't get their own load address at all.

Seed sourcing (per upstream docs, RISC-V path described explicitly; Arm path works on
the same principle via a platform hook): a hardware random seed is preferred
(`get_aslr_seed()`), falling back to a platform-specific `plat_get_aslr_seed()` hook; a
seed of zero disables randomization outright, which is also how deterministic/insecure
test builds pin the layout. TA-side ASLR instead calls `sys_gen_random_num()` when
mapping a TA's first segment, converting the randomness into a page offset bounded by
`CFG_TA_ASLR_MIN_OFFSET_PAGES`/`CFG_TA_ASLR_MAX_OFFSET_PAGES`, and degrades gracefully
to zero offset if the random mapping attempt fails rather than failing the TA load.

**Known incompatibility**: core ASLR and KASan are not usable together: don't expect
`CFG_CORE_ASLR=y` to coexist with a KASan-instrumented debug build.

## Stack canaries: core and TA are configured separately

Three mutually exclusive compiler-level settings, confirmed in `mk/config.mk:370-390`:

| Flag (core) | Flag (TA) | Compiler option | Default |
|---|---|---|---|
| `CFG_CORE_STACK_PROTECTOR` | `CFG_TA_STACK_PROTECTOR` | `-fstack-protector` | `n` |
| `CFG_CORE_STACK_PROTECTOR_STRONG` | `CFG_TA_STACK_PROTECTOR_STRONG` | `-fstack-protector-strong` | **`y`** |
| `CFG_CORE_STACK_PROTECTOR_ALL` | `CFG_TA_STACK_PROTECTOR_ALL` | `-fstack-protector-all` | `n` |

Both core and TA default to the "strong" variant (functions with local arrays,
`alloca()`, or address-taken locals get a canary; not literally every function the way
`-all` would). `config.mk` resolves whichever one is enabled via
`cfg-one-enabled` into `_CFG_CORE_STACK_PROTECTOR` / `_CFG_TA_STACK_PROTECTOR`.

**Core vs TA failure paths differ**:
- Core: guard value seeded via `plat_get_random_stack_canaries()`, stored in
  `__stack_chk_guard` (`lib/libutils/isoc/stack_check.c`); a smashed canary panics the
  whole system ("stack smashing detected").
- User-mode TA: lazily seeded on the TA's first entry (`__ta_entry()`), reused for the
  TA instance's lifetime; a smashed canary raises `TEE_ERROR_OVERFLOW` via
  `_utee_panic()` instead of panicking the whole secure world: the blast radius is
  contained to that one TA instance.
- **Pseudo-TAs follow the core's setting**, not the TA setting, since they share the
  core's address space and binary.

## Why this matters for contributions

A new driver or PTA shouldn't need to touch either of these flags: they're
core-wide/TA-wide defaults, not per-component. If a PR *does* change one of them,
that's a strong signal it needs the same design-first scrutiny as anything in
[[Secure Boot Chain of Trust]]'s territory (see the `optee-feature-design` skill, step
6).
