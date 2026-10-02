---
type: meta
title: "Hot Cache"
updated: 2026-05-22T00:00:00
tags:
  - meta
  - hot-cache
status: evergreen
related:
  - "[[index]]"
  - "[[log]]"
  - "[[Wiki Map]]"
  - "[[getting-started]]"
  - "[[DragonScale Memory]]"
---

# Recent Context

Navigation: [[index]] | [[log]] | [[overview]]

## Last Updated

2026-10-02 (even later): User reported the 5 OP-TEE canvases "not presented well" in Obsidian. Diagnosed 3 concrete bugs: (1) every `type:file` node was a *live note embed*, not a link card -- at 70-90px tall those previews were clipped to a sliver of frontmatter, which is what read as "cramped/clipped"; (2) the title card's x-position didn't span the actual diagram content (off-center, e.g. centered at x=-850 while the diagram sat between x=-700 and x=730), so it visually floated away from the graph; (3) no `type:group` zone backgrounds, so related nodes read as a flat scatter. Fixed all three across all 5 canvases: converted every file-embed node to a compact `**[[wikilink]]**` text card (same position/size, now actually a clickable link, no clipping), repositioned/resized each title to exactly span its diagram's group bounding box, and added 2-3 labeled `type:group` zones per canvas (colored, padded, inserted first in the node array so they render behind content). One real node-overlap bug surfaced during this: `optee-security-architecture.canvas`'s `keyhier` node sat at x=100, bridging between the hardening column (x=-130..150) and the storage column (x=440..720), so a rectangular zone around either column was geometrically impossible without overlap -- moved `keyhier`/`hashtree` into their own row under the crypto/storage column to resolve it. Verified post-fix: all 5 canvases parse as valid JSON, zero group/title overlaps (computed numerically, not eyeballed), and every `[[wikilink]]` in all 5 canvases resolves to a real wiki page title.

2026-10-02 (latest): Closed the OP-TEE learning-system task end to end. Built the 3 canvases flagged as the open "next step" in the prior entry: `optee-core-internals.canvas` (context graph: memory/pager/threading/interrupts, 9 nodes), `optee-security-architecture.canvas` (context graph: crypto/storage/key-hierarchy/boot-trust, 9 nodes), `optee-ta-lifecycle.canvas` (procedural graph: TA load through session teardown, 17 nodes) — all valid JSON, all referencing real entity/concept pages. OP-TEE domain now has 5 canvases total (2 from the first pass, 3 here) plus 41 wiki pages. Ran a full consistency pass: all wikilinks across `entities/optee/`, `concepts/optee/`, `sources/optee-*.md` resolve to real page titles (zero dangling links), all 5 canvases parse as valid JSON. Found and fixed one dangling link in the `optee-feature-design` skill (`[[OP-TEE License Header Requirements]]`, a page that was never created — license-header content actually lives inside `[[OP-TEE Coding Standards]]`) — pointed it there instead. The 3 Claude Code skills at `/home/bhaskarv/optee/.claude/skills/` (`optee-code-review`, `optee-feature-design`, `optee-contribution-workflow`) were already complete and verified sound: grounded in the real upstream docs and this checkout's own `checkpatch_inc.sh`/`typedefs.checkpatch`/`MAINTAINERS`, and all three gate risky actions (push/PR/force-push) on user confirmation rather than assuming blanket approval. Task (knowledge graphs + context graphs + procedural graphs + contribution skills for OP-TEE) is now fully delivered.

2026-10-02 (later): Completed the rest of the OP-TEE domain via 5 parallel fork agents, each covering one architecture area with a reserved address block (c-000060-064, 075-079, 090-093, 105-110, 120-123) to avoid collisions: core internals (memory/pager/threading/RPC/shared-memory/interrupts), Trusted Applications (pseudo-TA vs user-mode, ldelf loader, TA properties/session lifecycle), crypto + secure storage (crypto architecture, REE-FS/RPMB storage, key hierarchy HUK->SSK->TSK->FEK, hash-tree anti-rollback), client API + dev workflow (GP Client API model, xtest, TA library stack, [[optee_test]]/[[optee_examples]] entities), and platform/hardening (device tree, platform porting, ASLR/stack canaries, virtualization/SPMC). 24 new pages total, all grounded in real `optee_os`/`optee_client`/`optee_test` source (function/file names verified via grep, not guessed) plus the matching optee.readthedocs.io architecture page per topic. Found and fixed 2 broken wikilinks during merge ([[Libraries]], [[ldelf]] both pointed nowhere); verified zero em dashes and zero address collisions across all 24 files before integrating into index/concepts-index/entities-index/log. OP-TEE domain is now at 41 pages (17 from the first pass + 24 here), the most complete single-domain coverage in this vault. `wiki/sources/_index` untouched this pass (no new external docs ingested, only source-code cross-checks). Still open: GP TEE Internal Core API from the TA's own call-site point of view, and specific crypto algorithm implementations -- neither got a dedicated page. Canvases for these new areas not yet built (next step).

2026-10-02: Scaffolded a new OP-TEE learning domain (separate from this plugin's own dev history below) for a user learning OP-TEE and planning to contribute upstream. 17 new pages, addresses c-000043 through c-000059: entities in `wiki/entities/optee/` ([[OP-TEE Build Repo]], [[Trusted Firmware-A]], [[OP-TEE OS]], [[U-Boot]], [[Buildroot]], [[optee_client]], [[QEMU]]), concepts in `wiki/concepts/optee/` ([[OP-TEE Boot Flow]] hub, [[OP-TEE Build System]], [[Secure Boot Chain of Trust]], [[Normal World vs Secure World]], [[TEE Core Cold Boot]], [[OP-TEE Coding Standards]], [[OP-TEE Contribution Workflow]]), 3 source pages for fetched optee.readthedocs.io docs, 2 canvases (`optee-boot-flow.canvas` procedural, `optee-component-map.canvas` context graph). Content grounded in the user's real checkout at `/home/bhaskarv/optee/` (repo-tool manifest, real upstream git clones) plus live source inspection, not general knowledge. Retrofitted all new pages to remove em dashes per this vault's own style preference (see below). Next step (separate from this vault): three Claude Code skills for `/home/bhaskarv/optee` covering code review, feature design, and contribution workflow.

2026-05-22 (later): Batch-ingested a 5-source leadership-styles survey (The Muse, Harvard DCE, IMD, Managing Life at Work, Simply Psychology). 19 new pages, addresses c-000021 through c-000039: 5 source pages (flat in wiki/sources/), 11 concept pages in wiki/concepts/leadership-styles/ ([[Leadership Style]] hub, [[Lewin's Leadership Styles]], and styles autocratic/democratic/laissez-faire/transactional/transformational/servant/coaching/bureaucratic/situational), 3 entity pages in wiki/entities/leadership-styles/ ([[Kurt Lewin]], [[Bernard M. Bass]], [[Robert K. Greenleaf]]). First batch on the new source-subfolder convention. Shared thesis: no single best style, effectiveness is contextual, style is developable. Forbes and VeryWellMind block the Anthropic crawler and were NOT ingested (Goleman's six styles therefore absent). Vault now at 71 pages, 9 sources.

2026-05-22: Ingested [[nvme-base-spec-2.3]] (784pp, ratified July 2025). 6 new pages: [[NVMe]], [[NVMe Queue Model]], [[NVMe Namespaces]], [[NVMe over Fabrics]], [[NVM Express Consortium]], [[nvme-base-spec-2.3]]. Addresses c-000015 through c-000020 assigned. Wiki now covers storage-systems domain. Key new features in Rev 2.3: Flexible Data Placement (FDP), Track Memory Changes, TLS 1.3 for NVMe-TCP, ZNS updates. poppler-utils installed on this machine to enable PDF rendering. Pages reorganized into source-named subfolders: wiki/concepts/nvme/, wiki/entities/nvme/, wiki/concepts/courage-to-be-disliked/, wiki/entities/courage-to-be-disliked/. Sources remain flat in wiki/sources/. SKILL.md updated with Source Slug Derivation rules and new subfolder placement logic for all future ingests.

2026-05-21: Ingested [[courage-to-be-disliked]] (Hinglish PDF, 192 pages). 9 new pages: [[Alfred Adler]], [[Ichiro Kishimi]], [[Fumitake Koga]], [[Adlerian Psychology]], [[Teleology vs Etiology]], [[Separation of Tasks]], [[Community Feeling]], [[Inferiority Feelings]], [[courage-to-be-disliked]]. Addresses c-000006 through c-000014 assigned. Wiki now covers psychology domain (Adler/Kishimi/Koga) alongside its existing LLM/SEO domains. Also ran wiki-lint 2026-05-21: 20 issues found, 8 fixed (3 missing addresses, 5 dead-link fixes, 1 missing concept page E-commerce SEO created, 1 cross-ref gap). No orphan pages.

2026-04-24 (late night): v1.6.0 public release notes shipped. `docs/releases/v1.6.0.md` (Karpathy-style, 346 lines) establishes the release-notes convention. Three original SVGs at `wiki/meta/dragonscale-{mechanism-overview,6-test-flow,frontier-graph}.svg` carry the visual load; Wikipedia dragon curve referenced by text link only (no binary vendoring). R4 codex verifier ACCEPT WITH FIXES, 3 wording fixes applied. User runs `gh release create v1.6.0 --notes-file docs/releases/v1.6.0.md` when ready. Commits `85515bb` (docs), plus wiki/meta/ auto-commits for SVGs.

2026-04-24 (night): DragonScale end-to-end validation pass. Six-test menu run via Teams orchestration (codex gpt-5.4 for M1 dry-run, M1 commit, M4 autoresearch; chair for ollama pull, M2 allocate, M3 full tiling). All six green. First real fold committed (`wiki/folds/fold-k3-from-2026-04-23-to-2026-04-24-n8.md`, 115 lines, 8 children). First real tiling report at `wiki/meta/tiling-report-2026-04-24.md` (0 errors, 15 review pairs). M2 counter advanced 2 to 3, `c-000002` reserved-unassigned. M4 autoresearch filed 3 new concept pages (`Persistent Wiki Artifact`, `Source-First Synthesis`, `Query-Time Retrieval`) extending `[[How does the LLM Wiki pattern work]]` with Karpathy gist + RAG + MemGPT + Obsidian docs as sources. v1.6.0 validated.

2026-04-24 (evening): v1.6.0 closeout via Teams approach (chair-led, codex gpt-5.4 for sub-agents). 2 explorers (closeout gaps + doc surface). 6 bounded writes (non-overlapping scope): `docs/dragonscale-guide.md` (new, 563 lines), `wiki/meta/2026-04-24-v1.6.0-release-session.md` (new, 346 lines), `wiki/meta/boundary-frontier-2026-04-24.md` (first real M4 run artifact, new), `docs/install-guide.md` (1.5.0 to 1.6.0 + M4 callout + flat-extractive correction), `README.md` (parenthetical + guide link), `wiki/hot.md` (drift fixes). 1 adversarial verifier returned ACCEPT WITH FIXES; all 11 fixes applied in place. Docs commit `eb1562f`. `make test` green (74+ assertions). Still no git tags for v1.5.0 / v1.5.1 / v1.6.0. User requested gpt-5.5; API rejects it on this codex CLI; gpt-5.4 used throughout.

2026-04-24 (late): Phase 4 shipped. Mechanism 4 (boundary-first autoresearch) implemented as `scripts/boundary-score.py` with expanded test coverage. `/autoresearch` without a topic now offers frontier candidates (opt-in, agenda-control labeled). Cross-file status updated. Version bumped to 1.6.0 in `plugin.json` + `marketplace.json`; no git tag created locally (only pre-DragonScale tags `v1.1` - `v1.4.3` exist).

2026-04-24 (afternoon): Phase 3.6 hardening, five surgical fixes (tiling --report path confinement, rollout baseline, AGENTS.md consistency, wiki-ingest .raw contradiction, install-guide version). v1.5.1.

2026-04-24 (morning): Phase 3.5 hardening pass. Cross-phase audit resolved 10 hold-ship items. At that point Mechanism 4 was marked NOT IMPLEMENTED (later reversed in Phase 4 the same day). `bin/setup-dragonscale.sh` + tests + Makefile added, CHANGELOG created, versions synced to 1.5.0.

2026-04-23 (3): Phase 3 complete. Semantic tiling lint shipped as opt-in. `scripts/tiling-check.py` with flock-guarded atomic cache, localhost-locked OLLAMA_URL default, symlink rejection, model-drift invalidation, and banded thresholds (error>=0.90, review>=0.80, conservative seeds). 4 codex review rounds, 10/10 accept.

2026-04-23 (2): Phase 2 complete. Deterministic page addresses MVP via `scripts/allocate-address.sh` (flock-guarded, recovers counter from max observed). New frontmatter `address: c-NNNNNN`. `wiki-ingest` and `wiki-lint` updated with opt-in Address Assignment and Validation sections. 3 codex rounds, 8/8 accept.

2026-04-23 (1): Phase 0-1 complete. DragonScale Memory spec (`wiki/concepts/DragonScale Memory.md` v0.3) plus `skills/wiki-fold/` for Mechanism 1 (log rollups, dry-run verified). Survived multi-round codex review.

## Plugin State

- **Version**: 1.6.0 (Phase 4 shipped; plugin.json + marketplace.json synced; 1.5.1 was the Phase 3.6 hardening point release)
- **Install ID**: `claude-obsidian@claude-obsidian-marketplace`
- **Skills**: 11 (wiki, wiki-ingest, wiki-query, wiki-lint, wiki-fold, save, autoresearch, canvas, defuddle, obsidian-bases, obsidian-markdown)
- **Scripts**: `scripts/allocate-address.sh`, `scripts/tiling-check.py`, `scripts/boundary-score.py` (all opt-in; feature-detected by skills)
- **Setup**: `bin/setup-vault.sh` (base vault), `bin/setup-dragonscale.sh` (opt-in DragonScale), `bin/setup-multi-agent.sh` (multi-agent bootstrap)
- **Tests**: `make test` runs `tests/test_allocate_address.sh`, `tests/test_tiling_check.py`, `tests/test_boundary_score.py`. Zero ollama dependency for core tests.
- **Hooks**: 4 (SessionStart, PostCompact, PostToolUse [stages wiki/, .raw/, .vault-meta/], Stop)

## DragonScale Mechanisms

1. **Fold operator** (Mechanism 1): `skills/wiki-fold/`, dry-run verified AND first real fold committed at `wiki/folds/fold-k3-from-2026-04-23-to-2026-04-24-n8.md`.
2. **Deterministic addresses** (Mechanism 2): shipped and exercised; vault counter at 3. `c-000001` on DragonScale Memory.md. `c-000002` reserved-unassigned from validation pass (gap acceptable per spec).
3. **Semantic tiling lint** (Mechanism 3): shipped and activated. `nomic-embed-text` pulled; first tiling report at `wiki/meta/tiling-report-2026-04-24.md` (0 errors, 15 review-band pairs).
4. **Boundary-first autoresearch** (Mechanism 4): shipped (Phase 4, opt-in). `scripts/boundary-score.py` + `tests/test_boundary_score.py`. `/autoresearch` without a topic surfaces top-5 frontier pages as candidates; user picks, overrides, or declines. Explicitly labeled "agenda control" in both spec and skill.

## Key Lessons from This Release Cycle

1. Cross-phase audits are essential. Individual phase reviews miss drift between phases.
2. Opt-in feature detection (`[ -x script ] && [ -f state ]`) preserves default plugin behavior for adopters and non-adopters alike.
3. PostToolUse hook matcher is `Write|Edit`, so Bash writes don't fire it. Scripts that mutate tracked state must be Bash-only to avoid side-effect commits.
4. Seed-vault self-consistency matters: if the spec says post-rollout pages need addresses, the concept page itself has to have one.
5. Codex adversarial review rounds stop when the punch list is empty, not when the author feels done.

## Style Preferences

- No em dashes (U+2014) or `--` as punctuation. Periods, commas, colons, or parentheses. Hyphens in compound words are fine.
- Short and direct responses. No trailing summaries.
- Parallel tool calls when independent.

## Active Threads

- DragonScale Mechanism 4 shipped in Phase 4 as an opt-in Topic Selection mode in `skills/autoresearch/`. All four DragonScale mechanisms are now shipped and feature-gated.
- v1.6.0 not yet pushed to GitHub (local commits only, no git tag created). User controls push and tag timing.
- CLAUDE.md has one pre-existing uncommitted change ("Release Blog Post" section) that predates this session.

## Repo Locations

- Working: `~/Desktop/claude-obsidian/`
- Public: https://github.com/AgriciDaniel/claude-obsidian
