---
type: meta
title: "Wiki Index"
updated: 2026-04-07
tags:
  - meta
  - index
status: evergreen
related:
  - "[[overview]]"
  - "[[log]]"
  - "[[hot]]"
  - "[[dashboard]]"
  - "[[Wiki Map]]"
  - "[[concepts/_index]]"
  - "[[entities/_index]]"
  - "[[sources/_index]]"
  - "[[LLM Wiki Pattern]]"
  - "[[Hot Cache]]"
  - "[[Compounding Knowledge]]"
  - "[[Andrej Karpathy]]"
---

# Wiki Index

Last updated: 2026-10-02 | Total pages: 112 | Sources ingested: 10

Navigation: [[overview]] | [[log]] | [[hot]] | [[dashboard]] | [[Wiki Map]] | [[getting-started]]

---

## Concepts

- [[Leadership Style]] — hub: behavior patterns leaders adopt; no single best style, effectiveness is contextual (status: developing)
- [[Lewin's Leadership Styles]] — foundational 1939 typology: autocratic, democratic, laissez-faire (status: developing)
- [[Autocratic Leadership]] — leader decides alone, expects compliance; fast but stifling (status: developing)
- [[Democratic Leadership]] — participative, shared decision-making; most-cited style in the batch (status: developing)
- [[Laissez-Faire Leadership]] — delegative, hands-off; great for experts, harmful for dependent teams (status: developing)
- [[Transactional Leadership]] — rewards/penalties for performance; contingent reward + management by exception (status: developing)
- [[Transformational Leadership]] — inspire beyond self-interest toward a vision; Bass's four dimensions (status: developing)
- [[Servant Leadership]] — serve the team first; Greenleaf; claimed most effective in the batch (status: developing)
- [[Coaching Leadership]] — develop individuals' strengths; Nadella-at-Microsoft example (status: developing)
- [[Bureaucratic Leadership]] — rules, hierarchy, process; impersonal authority (status: developing)
- [[Situational Leadership]] — adapt style to the moment; the "leadership agility" thesis (status: developing)
- [[NVMe]] — Non-Volatile Memory Express; PCIe/Fabrics storage protocol; architecture, registers, command sets (status: developing)
- [[NVMe Queue Model]] — Submission Queue/Completion Queue pair mechanism; PRP/SGL data transfer; arbitration (status: developing)
- [[NVMe Namespaces]] — LBA address spaces; storage hierarchy; endurance groups; NVM sets; ANA (status: developing)
- [[NVMe over Fabrics]] — NVMe-oF; TCP/RDMA/FC transports; Discovery controller; connect/disconnect; TLS (status: developing)
- [[Adlerian Psychology]] — Individual Psychology; teleology, social interest, lifestyle, life tasks (status: developing)
- [[Teleology vs Etiology]] — Adler's core break from Freud: behavior explained by goals not causes (status: developing)
- [[Separation of Tasks]] — whose responsibility is this? Adlerian path to freedom in relationships (status: developing)
- [[Community Feeling]] — Gemeinschaftsgefuhl; belonging + contribution = happiness (status: developing)
- [[Inferiority Feelings]] — universal human driver; healthy feeling vs. pathological inferiority complex (status: developing)
- [[LLM Wiki Pattern]] — the pattern for building persistent, compounding knowledge bases using LLMs (status: mature)
- [[Hot Cache]] — ~500-word session context file, updated after every ingest and session (status: mature)
- [[Compounding Knowledge]] — why wiki knowledge grows more valuable over time, unlike RAG (status: mature)
- [[cherry-picks]] — prioritized feature backlog from ecosystem research; 13 features to add to claude-obsidian (status: current)
- [[SVG Diagram Style Guide]] — canonical visual style for all diagrams: Space Grotesk, #0A0A0A dark theme, #E07850 accent, full design tokens (status: evergreen)
- [[Pro Hub Challenge]] — community challenge pattern for building claude-seo/claude-blog extensions; first challenge produced 6 submissions, 5 integrated in v1.9.0 (status: evergreen)
- [[Semantic Topic Clustering]] — SERP-based keyword grouping replacing paid tools; hub-spoke architecture with interactive visualization (status: evergreen)
- [[Search Experience Optimization]] — "read SERPs backwards" methodology for page-type mismatch detection and persona scoring (status: evergreen)
- [[SEO Drift Monitoring]] — "git for SEO" baseline/diff/track with 17 comparison rules and SQLite persistence (status: evergreen)
- [[DragonScale Memory]] — memory-layer spec inspired by the Heighway dragon curve; fold operator, deterministic page addresses, semantic tiling, boundary-first autoresearch (status: shipped v0.4, all four mechanisms opt-in)
- [[Persistent Wiki Artifact]]: durable Markdown page as the LLM's memory object, distinct from ephemeral chat turns (status: developing)
- [[Source-First Synthesis]]: provenance discipline; raw sources stay immutable while the wiki layer is synthesized and cited (status: developing)
- [[Query-Time Retrieval]]: wiki query path synthesizes with citations; complementary to Obsidian's in-vault search (status: developing)
- [[OP-TEE Boot Flow]] — hub: BL1→BL2→BL32→BL33 chain for the qemu_v8 target; why BL32 is split into 3 images (status: developing)
- [[OP-TEE Build System]] — build/ repo's common.mk + per-platform .mk orchestration; the WSL PATH-with-spaces gotcha (status: developing)
- [[Secure Boot Chain of Trust]] — TF-A Trusted Board Boot cert chain (BL1→BL2→{BL32,BL33}) (status: developing)
- [[Normal World vs Secure World]] — ARM TrustZone EL3/S-EL1/EL1 split; SMC as the world-switch mechanism (status: developing)
- [[TEE Core Cold Boot]] — _start → boot_init_primary_early → init_primary → ... inside optee_os (status: developing)
- [[OP-TEE Coding Standards]] — checkpatch, GP CamelCase exception, mandatory variable init, SPDX headers (status: developing)
- [[OP-TEE Contribution Workflow]] — DCO/Signed-off-by, fork+PR, fixup→squash→tag→force-push cycle (status: developing)
- [[Memory Management]] — tee_mm physical allocator + core_mmu static mapping layer (status: developing)
- [[The Pager]] — demand-paging mechanism behind the BL32 3-image split (status: developing)
- [[Thread Model and RPC]] — per-SMC-call thread contexts, OPTEE_RPC_CMD_* round-trips to normal world (status: developing)
- [[Shared Memory Model]] — the mobj abstraction; client-registered vs RPC-payload memory sharing (status: developing)
- [[Interrupts and Notifications]] — hardware IRQs (GIC) vs async secure-to-normal notifications, two distinct mechanisms (status: developing)
- [[Pseudo-TA vs User-Mode TA]] — hub: trust/isolation model comparison (status: developing)
- [[ldelf TA Loader]] — two-stage ELF load: ldelf_load_ldelf → ldelf() → ta_elf_finalize_load_main (status: developing)
- [[TA Properties and Manifest]] — struct ta_head fields and their real semantics (status: developing)
- [[TA Session Lifecycle]] — tee_ta_manager.c's open/invoke/close + S-EL1→S-EL0 switch via user_ta_enter (status: developing)
- [[TA Storage and Loading]] — early/REE-FS/secure-storage TA sources, signature/encryption formats (status: developing)
- [[OP-TEE Crypto Architecture]] — crypto.h abstraction, LibTomCrypt (default) vs Mbed TLS, drvcrypt HW hook (status: developing)
- [[Secure Storage Architecture]] — REE FS vs RPMB backends, tee_svc_storage.c syscall layer (status: developing)
- [[Storage Key Hierarchy]] — HUK → SSK → TSK → FEK derivation chain (status: developing)
- [[Hash Tree Anti-Rollback]] — dual-versioned hash tree vs RPMB write-counter, what each protects against (status: developing)
- [[GlobalPlatform Client API Model]] — TEEC_* call sequence, Operation/Parameter/SharedMemory shapes (status: developing)
- [[xtest Test Framework]] — ADBG suite/case macros, numbered test-file ranges (status: developing)
- [[TA Library Stack]] — libutee/libutils/libmbedtls/libunw/libdl overview (status: developing)
- [[Example TA Structure]] — host/TA split pattern, four TA entry points, via hello_world (status: developing)
- [[Device Tree in OP-TEE]] — embedded/external/manifest DTB resolution order via get_dt()/get_secure_dt() (status: developing)
- [[Platform Porting]] — the three-file port layout + pre-upstream hardening checklist (status: developing)
- [[Hardening ASLR and Stack Canaries]] — CFG_CORE_ASLR/CFG_TA_ASLR, three stack-protector tiers (status: developing)
- [[Virtualization and SPMC]] — CFG_VIRTUALIZATION nexus model; SPMC_AT_EL=1/2/3 table (status: developing)

---

## Entities

- [[Kurt Lewin]] — social psychologist; 1939 study that founded the study of leadership styles (status: developing)
- [[Bernard M. Bass]] — scholar who formalized transformational vs transactional leadership (status: developing)
- [[Robert K. Greenleaf]] — coined servant leadership ("The Servant as Leader", 1970) (status: developing)
- [[NVM Express Consortium]] — standards body publishing the NVMe specification family (status: developing)
- [[Alfred Adler]] — Austrian psychiatrist (1870-1937); founder of Individual Psychology (status: developing)
- [[Ichiro Kishimi]] — Japanese philosopher, Adlerian counselor, co-author of The Courage to be Disliked (status: developing)
- [[Fumitake Koga]] — Japanese writer, co-author of The Courage to be Disliked (status: developing)
- [[Andrej Karpathy]] — AI researcher, creator of the LLM Wiki pattern, former Tesla AI director (status: developing)
- [[Ar9av-obsidian-wiki]] — multi-agent compatible LLM Wiki plugin; delta tracking manifest (status: current)
- [[Nexus-claudesidian-mcp]] — native Obsidian plugin + MCP bridge; workspace memory, task management (status: current)
- [[ballred-obsidian-claude-pkm]] — goal cascade PKM; auto-commit hooks, /adopt command (status: current)
- [[rvk7895-llm-knowledge-bases]] — 3-depth query system, Marp slides, parallel deep research (status: current)
- [[kepano-obsidian-skills]] — official skills from Obsidian creator; defuddle, obsidian-bases (status: current)
- [[Claudian-YishenTu]] — native Obsidian plugin embedding Claude Code; plan mode, @mention (status: current)
- [[Claude SEO]] — Tier 4 Claude Code skill for SEO analysis; 23 skills, 17 agents, 30 scripts at v1.9.0 (status: evergreen)
- [[OP-TEE Build Repo]] — github.com/OP-TEE/build; repo-tool manifest + Makefiles orchestrating ~10 sibling repos (status: developing)
- [[Trusted Firmware-A]] — BL1/BL2(/BL31); ARM's reference secure-boot firmware (status: developing)
- [[OP-TEE OS]] — the TEE itself, BL32; core/, ldelf/, lib/, ta/ (status: developing)
- [[U-Boot]] — BL33, normal-world bootloader (status: developing)
- [[Buildroot]] — builds the QEMU-target normal-world rootfs (status: developing)
- [[optee_client]] — libteec + tee-supplicant, GP Client API (status: developing)
- [[QEMU]] — emulated qemu_armv8a target board for this checkout (status: developing)
- [[optee_test]] — xtest runner + ta/ test-TA collection (status: developing)
- [[optee_examples]] — reference host/TA example pairs, hello_world/aes/acipher/secure_storage/etc. (status: developing)

---

## Sources

- [[leadership-styles-muse]] — 2026-05-22 | The Muse, Kat Boogaard | 10-style catalog
- [[determine-your-leadership-style-harvard]] — 2026-05-22 | Harvard DCE, Lian Parsons | style is not predetermined
- [[leadership-styles-imd]] — 2026-05-22 | IMD | 6 styles + leadership agility
- [[leadership-styles-managing-life-at-work]] — 2026-05-22 | research-grounded four-category taxonomy
- [[leadership-styles-simply-psychology]] — 2026-05-22 | Charlotte Nickerson | Lewin 1939 origin
- [[nvme-base-spec-2.3]] — 2026-05-22 | NVMe Base Spec Rev 2.3 (784pp) | 6 wiki pages created
- [[courage-to-be-disliked]] — 2026-05-21 | Koga + Kishimi (Hinglish) | 9 wiki pages created
- [[claude-obsidian-ecosystem-research]] — 2026-04-08 | web research across 16+ repos | 8 wiki pages created
- [[optee-contribute-guide]] — 2026-10-02 | optee.readthedocs.io | DCO, commit format, fork+PR+rebase workflow
- [[optee-coding-standards]] — 2026-10-02 | optee.readthedocs.io | checkpatch, GP CamelCase exception, variable init rule
- [[optee-license-headers]] — 2026-10-02 | optee.readthedocs.io | SPDX header rules for new/imported files

---

## Questions

- [[How does the LLM Wiki pattern work]] — how the pattern works and why it outperforms RAG at human scale (status: developing)

---

## Comparisons

- [[Wiki vs RAG]] — when to use a wiki knowledge base versus RAG; verdict: wiki wins at <1000 pages
- [[claude-obsidian-ecosystem]] — feature matrix of 16+ Claude+Obsidian projects; where claude-obsidian wins and gaps

---

## Decisions

- [[2026-04-14-community-cta-rollout]] - Skool community CTA footer added to 6 skill repos with per-tool frequency rules (status: active)
- [[2026-04-15-slides-and-release-session]] - Claude SEO v1.9.0 slides (15-slide HTML deck) + GitHub release v1.9.0 with PDF asset (status: complete)
- [[2026-04-15-release-report-session]] - Claude SEO v1.9.0 Release Report PDF: dark theme, 13 pages, WeasyPrint layout fixes, Challenge v2 added (status: complete)
- [[2026-04-14-claude-seo-v190-session]] - Claude SEO v1.9.0 Pro Hub Challenge integration: 5 submissions, 4 new skills, 4 review rounds, cybersecurity audit (status: complete)

---

## Domains

<!-- Add domain entries here after scaffold -->
