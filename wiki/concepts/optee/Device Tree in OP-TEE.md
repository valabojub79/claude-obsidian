---
type: concept
title: "Device Tree in OP-TEE"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - device-tree
  - boot
complexity: intermediate
domain: trusted-execution
status: developing
address: c-000120
related:
  - "[[OP-TEE Boot Flow]]"
  - "[[TEE Core Cold Boot]]"
  - "[[QEMU]]"
  - "[[Platform Porting]]"
sources:
  - "optee_os/core/kernel/dt.c"
  - "optee_os/mk/config.mk"
  - "optee_os/core/arch/arm/plat-vexpress/conf.mk"
  - "https://optee.readthedocs.io/en/latest/architecture/device_tree.html"
---

# Device Tree in OP-TEE

How [[OP-TEE OS]] learns what hardware it's running on, verified against
`optee_os/core/kernel/dt.c` and `mk/config.mk`, not just the docs.

## Three possible device trees, one resolution order

OP-TEE can draw platform description from up to three sources. `get_dt()`
(`core/kernel/dt.c:457`) tries them in this order:

1. **Embedded DTB** (`get_embedded_dt()`): compiled into OP-TEE's read-only section at
   build time. Requires `CFG_EMBED_DTB=y` plus `CFG_EMBED_DTB_SOURCE_FILE` pointing at
   a `.dts` under `core/arch/<arch>/dts/`.
2. **External DTB** (`get_external_dt()`): a non-secure-memory DTB whose physical
   address the bootloader hands to OP-TEE as a boot argument (or a fixed address via
   `CFG_DT_ADDR`).
3. **Manifest DTB** (`get_manifest_dt()`): a DT-formatted FF-A boot manifest, relevant
   only to the SPMC/virtualization paths (see [[Virtualization and SPMC]]).

`get_secure_dt()` is the same chain except it only falls through to the external DTB
if `CFG_MAP_EXT_DT_SECURE=y` (the upstream docs flag secure-only device trees as "not
implemented in the latest OP-TEE release", so treat `get_secure_dt()` on a real
platform as effectively returning the same external DTB as `get_dt()`, not a
genuinely separate secure-only tree, unless a specific platform wires that flag).

## Why non-secure vs secure matters

A DTB living in non-secure memory is readable by **both** worlds: OP-TEE can read
platform config from it during cold boot (see [[TEE Core Cold Boot]]), and the normal
world can read the same memory afterward. A DTB in secure-only memory would be
invisible to the normal world entirely, which is the whole point of putting
OP-TEE-private configuration there, but per above this path isn't generally available
yet.

## What OP-TEE does to the non-secure DTB

Before handing off to the normal world (see [[OP-TEE Boot Flow]]'s BL32 to BL33 step),
OP-TEE core adds to the external non-secure DTB:
- OP-TEE invocation-parameter nodes (so the normal-world driver in Linux knows how to
  reach OP-TEE).
- Reserved-memory nodes marking secure-only regions off-limits to the normal world.
- A PSCI node, if the DTB didn't already have one.

With `CFG_EXTERNAL_DTB_OVERLAY=y`, OP-TEE instead produces a DT **overlay** rather than
editing the tree directly: either appended into an existing overlay already in the
early-boot DTB, or written fresh at `CFG_DT_ADDR` for a later boot stage to merge (the
docs give [[U-Boot]] merging an OP-TEE overlay from TF-A as the canonical example,
which lines up with this checkout's own BL2 → BL32 → BL33 ordering).

## Real functions worth knowing (`core/kernel/dt.c`)

- `dt_find_compatible_driver()`, `dt_map_dev()`: how a driver locates and maps its node.
- `dt_enable_secure_status()` / `dt_disable_status()`: toggling a node's `status`
  property (e.g. hiding a device from the normal-world copy of the tree).
- `fdt_get_reg_props_by_index()`, `fdt_reg_info()`: reading a `reg` property; these are
  OP-TEE's own thin wrappers over libfdt, not libfdt itself.
- `fdt_get_status()`, `fdt_fill_device_info()`: populating `struct dt_node_info` for a
  given node offset.

## This checkout (qemu_v8 / plat-vexpress)

`core/arch/arm/plat-vexpress/conf.mk` forces `CFG_DT=y` (with `CFG_DTB_MAX_SIZE ?=
0x100000`) for the `qemu_virt`/`qemu_armv8a` flavors used by [[QEMU]]: this target
relies on an **external**, non-secure DTB from [[Trusted Firmware-A]]/[[U-Boot]], not
an embedded one, except when `CFG_DT_DRIVER_EMBEDDED_TEST=y` forces a test DTB
(`embedded_dtb_test.dts`) to be embedded purely for exercising the DT driver test
suite.

Related when writing a driver that needs to read platform config from DT: see
[[Platform Porting]] for the surrounding per-platform structure.
