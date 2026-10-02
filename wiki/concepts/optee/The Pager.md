---
type: concept
title: "The Pager"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - memory
  - pager
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000061
related:
  - "[[Memory Management]]"
  - "[[OP-TEE Boot Flow]]"
  - "[[OP-TEE OS]]"
  - "[[TEE Core Cold Boot]]"
sources:
  - "optee_os/core/arch/arm/mm/tee_pager.c"
  - "optee_os/core/include/mm/tee_pager.h"
---

# The Pager

Demand-paging for secure world. This is *why* [[OP-TEE Boot Flow]] splits BL32 into
three separate images (`bl32.bin` / `bl32_extra1.bin` / `bl32_extra2.bin`): the
pager is the mechanism that makes a "pageable" third image meaningful at all.
Lives in `optee_os/core/arch/arm/mm/tee_pager.c` (despite the `arch/arm/` path, this
is the generic pager, not an arm-specific detail).

## Why it exists

Secure SRAM is small on many real platforms. Instead of keeping all of OP-TEE OS's
code/data resident, the pageable part (`bl32_extra2.bin` = `tee-pageable_v2.bin`) is
kept in normal-accessible storage and only paged into secure RAM on demand, backed by
an encrypted/authenticated page store (a `struct fobj`, "file object", abstracts the
backing store for a page).

## Core mechanisms (verified against source)

- `tee_pager_early_init()`: sets up the pager before the rest of boot runs; called
  from [[TEE Core Cold Boot]]'s init sequence when `CFG_WITH_PAGER` is set.
- `tee_pager_add_core_region()`: registers a region of core (kernel) memory as
  pageable, associating it with a `vm_paged_region_type`.
- `tee_pager_add_um_region()` / `tee_pager_rem_um_region()` /
  `tee_pager_split_um_region()` / `tee_pager_merge_um_region()`: manage pageable
  regions belonging to a **u**ser **m**ode TA context (`struct user_mode_ctx`) as it
  loads, grows, or unloads.
- `tee_pager_handle_fault(struct abort_info *ai)`: the actual page-fault handler.
  Called from the data/prefetch abort path when a paged-but-not-currently-mapped
  address is touched; internally calls `pager_get_page()` to bring the page in
  (decrypt/verify from the `fobj` backing store, install a page-table entry) before
  returning so execution can resume.
- `tee_pager_set_alias_area()`: the pager uses a small fixed "alias" virtual window
  to temporarily map a physical page while copying/verifying its content, rather than
  mapping it at its final address immediately.

## Relationship to the static memory map

The pager doesn't replace [[Memory Management]]'s `core_mmu` static map: it manages
page-table entries *within* a region that map already carved out (via
`tee_pager_get_table_info()`, which hands back a `core_mmu_table_info` for the
affected page table). Pageable memory is still inside a `MEM_AREA_TA_RAM`-class
region; the pager just controls whether a given page inside it is currently resident.

## Practical note

`CFG_WITH_PAGER` is a build-time choice (see [[OP-TEE Build System]]); platforms with
enough secure RAM may disable it, which changes whether `bl32_extra1.bin`/
`bl32_extra2.bin` matter at all for that target. Check the platform's `conf.mk`
before assuming the pager is active.
