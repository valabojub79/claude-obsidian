---
type: concept
title: "Virtualization and SPMC"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - virtualization
  - spmc
  - ffa
complexity: advanced
domain: trusted-execution
status: developing
address: c-000123
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[Trusted Firmware-A]]"
  - "[[Normal World vs Secure World]]"
  - "[[OP-TEE OS]]"
sources:
  - "build/qemu_v8.mk"
  - "optee_os/mk/config.mk"
  - "https://optee.readthedocs.io/en/latest/architecture/virtualization.html"
  - "https://optee.readthedocs.io/en/latest/architecture/spmc.html"
---

# Virtualization and SPMC

[[OP-TEE Boot Flow]] documents the classic single-normal-world boot chain
(BL1 → BL2 → BL32 → BL33). This page covers the two ways that model gets more
complex: hypervisor-mediated virtualization, and the newer FF-A/SPMC architecture.
Both are **build-time alternatives** to the classic model, not additive features: a
given image is built one way or the other. `build/qemu_v8.mk`'s `SPMC_AT_EL` variable
(confirmed locally, lines ~29, 63-90, 239-250) is this checkout's concrete entry point
into the SPMC path; the classic path (`SPMC_AT_EL ?= n`, line 77) is what
[[OP-TEE Boot Flow]] describes.

## Virtualization (`CFG_VIRTUALIZATION`): one OP-TEE, many VMs

Problem solved: let a single OP-TEE instance serve multiple normal-world VMs, each
believing it has exclusive access, with hard isolation between them ("one VM can't
affect another in any way").

Mechanism: a hypervisor sits between the VMs and OP-TEE and does three things OP-TEE
itself can't do alone: tells OP-TEE when a VM is created (`OPTEE_SMC_VM_CREATED`) or
destroyed; translates each VM's intermediate physical addresses (IPA) to real physical
addresses; and pins shared-memory pages so they can't be swapped out from under an
in-flight secure call. Internally, OP-TEE splits into a **nexus** (core SMC
handling/memory management, always mapped) plus one **TEE instance per VM** (mapped
only while that VM is actually calling in): this reuses existing TEE code rather than
rewriting it per-VM, at the cost of "banked" memory sections.

Key flags: `CFG_VIRTUALIZATION=y` (OP-TEE then *requires* a compatible hypervisor to
boot at all), `CFG_VIRT_GUEST_COUNT` (fixed VM count; memory is split equally across
all guests specifically to prevent one greedy VM from starving the others, i.e. a
DoS-prevention design choice, not just a sizing default).

Current limits per upstream docs: Armv8-A only, static/equal-split memory allocation,
most hardware accelerators unavailable (serial console being the exception), and XEN
is the hypervisor with actual OP-TEE mediator support today.

## SPMC/SPMD: the FF-A path

Separate axis from virtualization. The Firmware Framework for Arm (FF-A) defines a
Secure Partition Manager split into a **Dispatcher (SPMD)**, always at EL3 (inside
[[Trusted Firmware-A]]), and a **Controller (SPMC)**, which can live at one of three
levels depending on `SPMC_AT_EL` (naming and semantics confirmed directly in
`build/qemu_v8.mk`'s comments):

| `SPMC_AT_EL` | SPMC location | SPMD location |
|---|---|---|
| `3` | EL3, alongside the SPMD (TF-A does both) | EL3 (TF-A) |
| `2` | S-EL2, in **Hafnium** | EL3 (TF-A) |
| `1` | S-EL1, **inside OP-TEE OS itself** | EL3 (TF-A) |

`SPMC_AT_EL=1` is the one directly relevant to this checkout: OP-TEE OS *is* the SPMC,
and TF-A's BL2 passes it a manifest DTB (`spmc_el1_manifest_*.dts`, visible as one of
the `ln -sf` targets in [[OP-TEE Boot Flow]]'s symlink block) describing the Secure
Partitions to load. `SPMC_AT_EL=2` instead builds **Hafnium** as a separate BL32-slot
binary (`HAFNIUM_BIN`, built from a sibling `hafnium/` repo this build manifest can
pull in) acting as the SPMC at S-EL2, with OP-TEE OS itself becoming just one Secure
Partition among potentially several, rather than the SPMC.

### How this changes the boot-time handoff

In the classic model ([[OP-TEE Boot Flow]]), BL32 cold-boots once and then idles
waiting for SMCs. Under SPMC_AT_EL=1, OP-TEE OS additionally runs `sp_init_all()`
during its `boot_final` init step (see [[TEE Core Cold Boot]] for where
`boot_init_primary_final()` sits in that sequence) to start every Secure Partition
described in the manifest: these SP images are either embedded in the OP-TEE image
or loaded from TF-A's FIP by BL2, so they're available before the normal world ever
boots. Once SP startup finishes, OP-TEE/the SPMC sends `FFA_MSG_WAIT` to hand control
back to the normal world, functionally replacing the plain "idle waiting for SMC"
end-state of the classic cold boot with "idle waiting for an FF-A message." From
BL33's perspective the visible difference is which messages the secure side now
understands (FF-A direct/indirect messages, not just raw OP-TEE SMCs), handled via
[[Normal World vs Secure World]]'s existing SMC mechanism underneath.

## Relationship between the two axes

Virtualization and SPMC solve different problems (many normal-world VMs vs.
many secure-world partitions) and are configured independently, though both move
OP-TEE away from the single-tenant, single-SMC-dispatcher model that
[[OP-TEE Boot Flow]] describes as the default. A platform port combining both would
need a hypervisor that also understands FF-A, not just OPTEE_SMC_VM_CREATED, a
detail worth confirming against current `optee_os/mk/config.mk` dependency rules
(`CFG_CORE_SEL1_SPMC`/`CFG_CORE_SEL2_SPMC` interactions with `CFG_VIRTUALIZATION`)
rather than assumed, since this page didn't verify that combination exists in
practice.
