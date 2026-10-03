---
type: meta
title: "Concepts Index"
updated: 2026-04-07
tags:
  - meta
  - index
  - concept
domain: knowledge-management
status: evergreen
related:
  - "[[index]]"
  - "[[dashboard]]"
  - "[[Wiki Map]]"
  - "[[Hot Cache]]"
  - "[[LLM Wiki Pattern]]"
  - "[[Compounding Knowledge]]"
  - "[[LLM Wiki Pattern]]"
  - "[[Hot Cache]]"
  - "[[Compounding Knowledge]]"
---

# Concepts Index

Navigation: [[index]] | [[entities/_index|Entities]] | [[sources/_index|Sources]]

All concept pages — ideas, patterns, and frameworks extracted from sources.

---

## Knowledge Management

- [[LLM Wiki Pattern]] — the core architecture for persistent, compounding knowledge bases
- [[Hot Cache]] — ~500-word session context file, updated after every ingest
- [[Compounding Knowledge]] — why the wiki grows more valuable over time, unlike RAG
- [[DragonScale Memory]] — memory-layer spec: fold operator, deterministic page addresses, semantic tiling, boundary-first autoresearch (status: shipped v0.4, all four mechanisms opt-in)
- [[Persistent Wiki Artifact]]: durable Markdown page as the LLM's memory object (developing)
- [[Source-First Synthesis]]: provenance discipline for LLM wiki layers (developing)
- [[Query-Time Retrieval]]: query synthesis with citations, complementary to Obsidian search (developing)

---

## Storage Systems

- [[NVMe]] — Non-Volatile Memory Express; PCIe+Fabrics storage protocol; queue model, namespaces, extended capabilities (developing)
- [[NVMe Queue Model]] — SQ/CQ ring buffer mechanism; PRP/SGL data transfer; doorbell; arbitration (developing)
- [[NVMe Namespaces]] — LBA spaces; endurance groups; NVM sets; ANA multi-path access (developing)
- [[NVMe over Fabrics]] — NVMe-oF; TCP/RDMA/FC transports; discovery; TLS 1.3; DH-HMAC-CHAP (developing)

---

## Psychology

- [[Adlerian Psychology]] — Individual Psychology; teleology, social interest, life tasks, lifestyle (developing)
- [[Teleology vs Etiology]] — Adler's core break from Freud: behavior explained by goals, not causes (developing)
- [[Separation of Tasks]] — whose responsibility is this? The Adlerian path to interpersonal freedom (developing)
- [[Community Feeling]] — Gemeinschaftsgefuhl; belonging + contribution as the definition of happiness (developing)
- [[Inferiority Feelings]] — universal human driver; healthy feeling vs. pathological inferiority complex (developing)

---

## Leadership

Five-source survey ingested 2026-05-22. Pages live in `wiki/concepts/leadership-styles/`.

- [[Leadership Style]] — hub: behavior patterns leaders adopt; no single best style; the four-category taxonomy and cross-source map (developing)
- [[Lewin's Leadership Styles]] — foundational 1939 typology: autocratic, democratic, laissez-faire (developing)
- [[Autocratic Leadership]] — leader decides alone, expects compliance (developing)
- [[Democratic Leadership]] — participative, shared decision-making (developing)
- [[Laissez-Faire Leadership]] — delegative, hands-off (developing)
- [[Transactional Leadership]] — rewards/penalties for performance (developing)
- [[Transformational Leadership]] — inspire beyond self-interest toward a vision (developing)
- [[Servant Leadership]] — serve the team first; Greenleaf (developing)
- [[Coaching Leadership]] — develop individuals' strengths (developing)
- [[Bureaucratic Leadership]] — rules, hierarchy, process (developing)
- [[Situational Leadership]] — adapt style to the moment; leadership agility (developing)

---

## Trusted Execution (OP-TEE)

Ingested 2026-10-02 in two passes: boot flow/build system first, then a parallel deep
pass covering the rest of OP-TEE's architecture. Pages live in `wiki/concepts/optee/`.
Hub page for the whole domain: [[OP-TEE Boot Flow]].

**Boot & build**
- [[OP-TEE Boot Flow]] — hub: BL1→BL2→BL32→BL33 chain for the qemu_v8 target; why BL32 is split into 3 images (developing)
- [[OP-TEE Build System]] — build/ repo's common.mk + per-platform .mk orchestration; the WSL PATH-with-spaces gotcha (developing)
- [[Secure Boot Chain of Trust]] — TF-A Trusted Board Boot cert chain (developing)
- [[Normal World vs Secure World]] — ARM TrustZone EL3/S-EL1/EL1 split; SMC as the world-switch mechanism (developing)
- [[TEE Core Cold Boot]] — _start → boot_init_primary_early → init_primary → ... inside optee_os, traced from source (developing)

**Core internals**
- [[Memory Management]] — tee_mm physical allocator + core_mmu static mapping layer (developing)
- [[The Pager]] — demand-paging mechanism behind the BL32 3-image split (developing)
- [[Thread Model and RPC]] — per-SMC-call thread contexts, OPTEE_RPC_CMD_* round-trips to normal world (developing)
- [[Shared Memory Model]] — the mobj abstraction; client-registered vs RPC-payload memory sharing (developing)
- [[Interrupts and Notifications]] — hardware IRQs (GIC) vs async secure-to-normal notifications (developing)

**Trusted Applications**
- [[Pseudo-TA vs User-Mode TA]] — hub: trust/isolation model comparison (developing)
- [[ldelf TA Loader]] — two-stage ELF load: ldelf_load_ldelf → ldelf() → ta_elf_finalize_load_main (developing)
- [[TA Properties and Manifest]] — struct ta_head fields and their real semantics (developing)
- [[TA Session Lifecycle]] — open/invoke/close + S-EL1→S-EL0 switch via user_ta_enter (developing)
- [[TA Storage and Loading]] — early/REE-FS/secure-storage TA sources, signature/encryption formats (developing)
- [[Example TA Structure]] — host/TA split pattern, four TA entry points, via hello_world (developing)
- [[TA Library Stack]] — libutee/libutils/libmbedtls/libunw/libdl overview (developing)

**Crypto & secure storage**
- [[OP-TEE Crypto Architecture]] — crypto.h abstraction, LibTomCrypt (default) vs Mbed TLS, drvcrypt HW hook (developing)
- [[Secure Storage Architecture]] — REE FS vs RPMB backends, tee_svc_storage.c syscall layer (developing)
- [[Storage Key Hierarchy]] — HUK → SSK → TSK → FEK derivation chain (developing)
- [[Hash Tree Anti-Rollback]] — dual-versioned hash tree vs RPMB write-counter (developing)

**Client API & testing**
- [[GlobalPlatform Client API Model]] — TEEC_* call sequence, Operation/Parameter/SharedMemory shapes (developing)
- [[xtest Test Framework]] — ADBG suite/case macros, numbered test-file ranges (developing)

**Platform & hardening**
- [[Device Tree in OP-TEE]] — embedded/external/manifest DTB resolution order (developing)
- [[Platform Porting]] — the three-file port layout + pre-upstream hardening checklist (developing)
- [[Hardening ASLR and Stack Canaries]] — CFG_CORE_ASLR/CFG_TA_ASLR, three stack-protector tiers (developing)
- [[Virtualization and SPMC]] — CFG_VIRTUALIZATION nexus model; SPMC_AT_EL=1/2/3 table (developing)

**Contribution**
- [[OP-TEE Coding Standards]] — checkpatch, GP CamelCase exception, mandatory variable init, SPDX headers (developing)
- [[OP-TEE Contribution Workflow]] — DCO/Signed-off-by, fork+PR, fixup→squash→tag→force-push cycle (developing)

---

## Add new concepts here as they are extracted from sources.
