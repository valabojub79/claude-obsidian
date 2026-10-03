---
type: concept
title: "OP-TEE Boot Flow"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - boot
  - hub
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000053
related:
  - "[[QEMU]]"
  - "[[Trusted Firmware-A]]"
  - "[[OP-TEE OS]]"
  - "[[U-Boot]]"
  - "[[Buildroot]]"
  - "[[Secure Boot Chain of Trust]]"
  - "[[Normal World vs Secure World]]"
  - "[[TEE Core Cold Boot]]"
  - "[[OP-TEE Build System]]"
sources:
  - "build/qemu_v8.mk"
---

# OP-TEE Boot Flow

**Hub page.** The BL1→BL2→BL32→BL33 chain is the backbone everything else in this domain hangs off. Terminology (BL1/BL2/BL32/BL33) comes from [[Trusted Firmware-A]]'s "Boot Loader stage" naming, which OP-TEE's build system adopts directly.

## The chain (qemu_v8 target)

```
QEMU (-bios bl1.bin)
   │  loads BL1 into SRAM, jumps to it at EL3
   ▼
BL1  (Trusted Firmware-A)
   │  loads + authenticates BL2 from flash/FIP
   ▼
BL2  (Trusted Firmware-A)
   │  loads + authenticates BL32 (secure) and BL33 (non-secure) images,
   │  then hands off to BL32 FIRST
   ▼
BL32  (OP-TEE OS: secure world, S-EL1)
   │  cold-boots the TEE kernel (see [[TEE Core Cold Boot]]),
   │  then returns control to Normal World
   ▼
BL33  (U-Boot: normal world)
   │  loads Linux kernel + Buildroot rootfs, boots to userspace
   ▼
Linux userspace (optee_client's tee-supplicant, xtest, examples, ...)
```

Authentication at the BL1→BL2 and BL2→{BL32,BL33} steps is covered separately in [[Secure Boot Chain of Trust]]. The EL3/S-EL1/EL1-normal split and how execution moves between them (SMC) is covered in [[Normal World vs Secure World]].

## Why BL32 is split into three files

OP-TEE OS supports demand-paging TA code/data that doesn't need to be resident. Its build produces three images under `optee_os/out/arm/core/`:

| Build output | Symlinked as (`out/bin/`) | Contents |
|---|---|---|
| `tee-header_v2.bin` | `bl32.bin` | Fixed init/unpaged core: always resident |
| `tee-pager_v2.bin` | `bl32_extra1.bin` | Pager-managed init pages |
| `tee-pageable_v2.bin` | `bl32_extra2.bin` | Pageable core/TA pages, loaded on demand |

`build/qemu_v8.mk` (~line 283-310) is what creates these three symlinks plus `bl1.bin`, `bl2.bin`, and `bl33.bin` (→ [[U-Boot]]'s `u-boot.bin`): this is the exact `ln -sf ...` block that appears at the top of every OP-TEE QEMU build log, including the one that kicked off this whole learning project.

## Starting point to go deeper

- Build orchestration that produces these binaries: [[OP-TEE Build System]]
- What BL32 actually does on entry: [[TEE Core Cold Boot]]
