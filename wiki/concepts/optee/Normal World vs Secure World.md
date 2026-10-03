---
type: concept
title: "Normal World vs Secure World"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - arm-trustzone
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000056
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[OP-TEE OS]]"
  - "[[Trusted Firmware-A]]"
  - "[[optee_client]]"
sources:
  - "optee_os/core/arch/arm/kernel/thread.c"
---

# Normal World vs Secure World

ARM TrustZone splits the CPU into two "worlds" via the `NS` (non-secure) bit, each with its own exception levels:

| World | Exception levels in play | Who runs there |
|---|---|---|
| Secure | EL3 (monitor) + S-EL1 | [[Trusted Firmware-A]]'s BL31/EL3 runtime; [[OP-TEE OS]] at S-EL1 |
| Normal (non-secure) | EL2/EL1 | [[U-Boot]], Linux kernel, [[optee_client]] userspace |

## How execution moves between worlds

A **Secure Monitor Call (SMC)** triggers a world switch via the EL3 monitor. Normal-world code (the Linux `optee` kernel driver, via [[optee_client]]'s `libteec`) issues an SMC to invoke a TA; the EL3 monitor routes it into OP-TEE OS at S-EL1, which dispatches it to the right Trusted Application; OP-TEE OS returns via another SMC back through EL3 to Normal World. On the OP-TEE OS side, this entry/exit/dispatch logic lives in `optee_os/core/arch/arm/kernel/thread.c`.

## Relevance to the boot flow

In [[OP-TEE Boot Flow]], BL2 (still effectively straddling both, pre-split) explicitly boots BL32 (secure) *before* BL33 (normal): secure world must be initialized and ready to receive SMCs before normal world ever gets a chance to issue one.
