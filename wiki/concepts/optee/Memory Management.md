---
type: concept
title: "Memory Management"
created: 2026-10-02
updated: 2026-10-02
tags:
  - concept
  - optee
  - trusted-execution
  - memory
  - core-internals
complexity: advanced
domain: trusted-execution
status: developing
address: c-000060
related:
  - "[[OP-TEE OS]]"
  - "[[The Pager]]"
  - "[[TEE Core Cold Boot]]"
  - "[[Shared Memory Model]]"
sources:
  - "optee_os/core/mm/tee_mm.c"
  - "optee_os/core/mm/core_mmu.c"
  - "https://optee.readthedocs.io/en/latest/architecture/core.html"
---

# Memory Management

How [[OP-TEE OS]] tracks and maps physical memory inside secure world. Two layers
sit under everything else here: a flat physical allocator (`tee_mm`), and the
MMU/virtual-mapping layer (`core_mmu`). Demand-paging on top of these is a separate,
larger mechanism, covered in [[The Pager]].

## tee_mm: the physical allocator

`core/mm/tee_mm.c` implements `tee_mm_pool_t`, a simple first-fit allocator over a
physical address range. Key functions (verified against source):

- `tee_mm_init(pool, lo, size, ...)`: carve out a pool from a base address + size.
- `tee_mm_alloc_flags()` / `tee_mm_alloc2()`: allocate an aligned region (`tee_mm_entry_t`)
  from a pool, either anywhere or at a fixed base.
  `tee_mm_free()`: release one back.

OP-TEE OS sets up separate pools for distinct physical regions (TA RAM, core heap,
etc.) at boot, via [[TEE Core Cold Boot]]'s `init_primary()`. This is deliberately a
flat allocator with no notion of virtual addresses. That's `core_mmu`'s job.

## core_mmu: the mapping layer

`core/mm/core_mmu.c` owns `struct tee_mmap_region`, the table of static
physical-to-virtual mappings OP-TEE OS sets up at boot (one entry per memory type:
`MEM_AREA_TEE_RAM`, `MEM_AREA_TA_RAM`, device memory windows, etc.). Lookups go
through `find_map_by_type()`, `find_map_by_va()`, `find_map_by_pa()`; the memory map
itself is merged/deduplicated at boot via `merge_mmaps()` and `mmaps_are_mergeable()`
before being committed.

This static map is what the pager's `core_mmu_table_info` interacts with when it
installs or evicts page-table entries for a paged region. See [[The Pager]] for how
individual pages move in and out of that static map's TA RAM window.

## Where this fits in the bigger picture

- Memory *allocation* (tee_mm) is separate from memory *mapping* (core_mmu) is
  separate from memory *paging* (tee_pager, see [[The Pager]]). A given TA's memory
  footprint touches all three.
- Shared memory registered by normal world (see [[Shared Memory Model]]) is deliberately
  **not** part of this allocator: it's memory normal world owns, that secure world
  maps temporarily, not memory secure world allocates from its own pools.
