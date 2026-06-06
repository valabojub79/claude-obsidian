---
type: meta
title: "Lint Report 2026-06-06"
created: 2026-06-06
updated: 2026-06-06
tags: [meta, lint]
status: developing
---

# Lint Report: 2026-06-06

Run after the 5-source leadership-styles batch ingest (c-000021 through c-000039).

## Summary
- Pages scanned: 82 (.md under `wiki/`)
- Issues found: 8 actionable (3 dead-link clusters, 1 missing nav page, 2 frontmatter gaps, plus informational items)
- Auto-fixed: 3 (created `Wiki Map.md`; added `created`/`updated` to `nvme-base-spec-2.3` and `courage-to-be-disliked`)
- Needs review: 2 dead-link clusters left intentionally (historical session note + fold-page tooling refs)
- **The leadership-styles batch is clean**: 0 orphans, 0 dead links, 0 address errors, 0 frontmatter gaps among the 19 new pages.

> [!note] Note on link styling in this report
> Page names referenced as examples below are written in backticks, not live `[[wikilinks]]`, so this report does not itself introduce the dead links it describes.

## Orphan Pages
None. Every non-meta page has at least one inbound wikilink.

## Dead Links

Genuine (all pre-existing, none from this batch):

- **[[Wiki Map]]** — referenced in [[getting-started]], [[hot]], [[index]] (x2), [[concepts/_index]], and in many pages' `related:` frontmatter, but `wiki/Wiki Map.md` does not exist. This is the highest-value fix: it is a navigation target across the vault. Suggest: create a `Wiki Map` page (or remove the references).
- **[[Claude Obsidian]]**, **[[Claude Canvas]]**, **[[Rankenstein]]**, **[[Karpathy LLM Wiki Pattern]]** — all in the historical note `wiki/meta/2026-04-10-backlink-empire-session.md`. Suggest: leave as-is (session notes are point-in-time) or convert to plain text.
- **[[wiki-fold]]** (x3), **[[fold-template]]** — in `wiki/folds/fold-k3-...md`; these name a skill and a template, not wiki pages. Suggest: leave (they document tooling) or unlink.

False positives (link resolves to a non-`.md` file, no action):

- [[dashboard.base]] — resolves to `wiki/meta/dashboard.base`.
- [[claude-obsidian-presentation]] — resolves to `wiki/canvases/claude-obsidian-presentation.canvas`.

## Missing Pages (informational, by design)

The [[Leadership Style]] hub catalogs several styles that appear in only one or two sources and were intentionally not given their own page:

- **Visionary / Authoritative** (mentioned in [[determine-your-leadership-style-harvard]] and [[leadership-styles-imd]], 2 sources) — the strongest candidate for promotion to its own page if a third source arrives.
- Charismatic, Pacesetter, Strategic, Empowering, Ethical, Authentic — single-source each; cataloged in the hub.

No action needed unless a future ingest adds corroborating sources.

## Frontmatter Gaps

- [[nvme-base-spec-2.3]]: missing `created`, `updated` (pre-existing, from the 2026-05-22 NVMe ingest).
- [[courage-to-be-disliked]]: missing `created`, `updated` (pre-existing, from the 2026-05-21 ingest).

## Stale Claims / Contradictions
None new. One intentional `> [!contradiction]` callout exists on [[Laissez-Faire Leadership]] (practitioner sources call it empowering; the academic source calls it "severely detrimental") — this is a documented tension, not a defect.

## Cross-Reference Gaps
None. Entity mentions ([[Kurt Lewin]], [[Bernard M. Bass]], [[Robert K. Greenleaf]]) are linked wherever they appear in prose.

## Address Validation
- Counter state (`--peek`): 40
- Highest c- address observed: c-000039
- Addressed pages: 38 (all valid `c-NNNNNN` format, 0 duplicates, 0 drift)
- Post-rollout pages checked: all passing
- `address_map` consistency: 38/38 entries resolve to existing files with matching frontmatter. 0 mismatches.
- `c-000002` remains reserved-unassigned (gap acceptable per spec).

## Semantic Tiling
Skipped: ollama not reachable (`tiling-check.py --peek` exit 10). Re-run with ollama up and `nomic-embed-text` pulled to check the new leadership cluster for near-duplicates (the nine style pages are the most likely review-band candidates).

## Naming / Style
- New subfolder convention applied correctly: leadership concept/entity pages live under `wiki/concepts/leadership-styles/` and `wiki/entities/leadership-styles/`; source summaries stay flat in `wiki/sources/`. Folder name is lowercase-with-dashes per convention.
- No em-dash/`--` punctuation violations found in the new pages.
