---
type: concept
title: "Secure Boot Chain of Trust"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - secure-boot
  - arm-trustzone
complexity: advanced
domain: trusted-execution
status: developing
address: c-000055
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[Trusted Firmware-A]]"
  - "[[OP-TEE OS]]"
sources:
  - "https://optee.readthedocs.io/en/latest/architecture/secure_boot.html"
---

# Secure Boot Chain of Trust

Each boot stage in [[OP-TEE Boot Flow]] should cryptographically verify the next before handing off to it: that's what makes it a *chain of trust* rather than just a chain of hand-offs.

## Armv8-A path (this checkout's target): TF-A's Trusted Board Boot (TBB)

[[Trusted Firmware-A]] implements its own authentication framework (TBB / "Trusted Board Boot"). When enabled, BL1 verifies BL2's signature before running it, and BL2 in turn verifies BL32 and BL33 using a certificate chain rooted at a trusted key: the `trusted_key.crt`, `tb_fw.crt`, `tos_fw_key.crt`/`tos_fw_content.crt` (TOS = BL32), `nt_fw_key.crt`/`nt_fw_content.crt` (NT = BL33), `soc_fw_key.crt`/`soc_fw_content.crt` files visible in `trusted-firmware-a/build/qemu/release/` and symlinked by `build/qemu_v8.mk`. Whether TBB is actually *enforced* (vs. images just being present but unsigned/unverified) is a TF-A build-time config choice: worth checking the specific `trusted-firmware-a` build flags (`TRUSTED_BOARD_BOOT=1`, `GENERATE_COT=1`) in this checkout rather than assuming.

## Armv7-A path

Platforms without TF-A (older Armv7-A SoCs) can't rely on TBB, so OP-TEE itself may provide an alternative authentication framework at that boundary instead: details are platform-specific; see the upstream architecture doc for specifics per SoC.

## Why this matters for contributions

Anything touching boot-stage image format, certificate generation, or the BL2→BL32 handoff is security-sensitive by definition: this is exactly the kind of area where a design proposal (not just a PR) is the right first move, and where [[OP-TEE Contribution Workflow]]'s review bar is highest.
