---
type: meta
title: "Lint Report 2026-05-21"
created: 2026-05-21
updated: 2026-05-21
tags: [meta, lint]
status: developing
---

# Lint Report: 2026-05-21

## Summary

- Pages scanned: 46 (25 non-meta/non-excluded)
- Issues found: 20
- Auto-fixed: 0
- Needs review: 20

| Category | Count | Severity | Status |
|---|---|---|---|
| Dead links (actionable) | 4 | error | fixed |
| Dead links (meta/fold pages) | 11 | informational | left as-is |
| Missing address (post-rollout) | 3 | error | fixed |
| Empty sections | 0 | - | false positives (code blocks) |
| Missing pages | 1 | warning | fixed (stub created) |
| Cross-reference gaps | 1 | informational | fixed |
| Orphan pages | 0 | - | - |
| Frontmatter gaps | 0 | - | - |
| Stale index entries | 0 | - | - |
| Address format/uniqueness errors | 0 | - | - |

---

## Dead Links

### Errors (non-meta pages)

**`[[How does the LLM Wiki pattern work?]]` - trailing `?` typo**

The file is `wiki/questions/How does the LLM Wiki pattern work.md` (no `?` in filename). Wikilinks with a trailing `?` do not resolve. Appears in 5 pages:

- `wiki/hot.md` - body text reference
- `wiki/log.md` - body text reference
- `wiki/concepts/Source-First Synthesis.md` - `related:` frontmatter
- `wiki/concepts/Persistent Wiki Artifact.md` - `related:` frontmatter
- `wiki/concepts/Query-Time Retrieval.md` - `related:` frontmatter

Fix: remove the trailing `?` from the wikilink in all 5 locations.

**Test placeholders left in production pages**

- `wiki/concepts/DragonScale Memory.md`: `[[Foo]]` and `[[notes/Foo]]` - example links from the spec, never created.
- `wiki/log.md`: `[[notes/Foo]]` - same.

Fix: remove or replace with real pages.

**Missing concept page**

- `wiki/entities/Claude SEO.md` references `[[E-commerce SEO]]` but no such page exists.

Suggest: create `wiki/concepts/E-commerce SEO.md` stub, or replace the link with a plain mention if the page is out of scope.

**Legacy canvas reference**

- `wiki/overview.md` references `[[AI Marketing Hub Cover Images Canvas]]`. No `.canvas` file by that name exists in the vault.

Suggest: remove the link or create the canvas.

### Informational (meta and fold pages)

These are in session-log or fold files. They represent historical context or skill references; no immediate fix required.

- `wiki/meta/2026-04-10-backlink-empire-session.md`: `[[Claude Obsidian]]`, `[[Claude Canvas]]`, `[[Rankenstein]]`, `[[Karpathy LLM Wiki Pattern]]` - external project references from that session.
- `wiki/meta/2026-04-14-claude-seo-v190-session.md`: `[[E-commerce SEO]]` - same concept as above.
- `wiki/folds/fold-k3-from-2026-04-23-to-2026-04-24-n8.md`: `[[wiki-fold]]` (x3), `[[fold-template]]` - fold file references the skill directory and a template that does not exist as a wiki page.
- `wiki/concepts/cherry-picks.md`: `[[wikilinks]]` - possibly a test mention.
- `wiki/concepts/Persistent Wiki Artifact.md`: `[[Three laws of motion]]` - appears to be an illustrative reference rather than an intended page.

---

## Address Validation

- Counter state: `3` (next address: `c-000003`)
- Highest `c-` address observed: `c-000001` (on `concepts/DragonScale Memory.md`)
- `c-000002`: reserved-unassigned from 2026-04-24 validation pass (gap is acceptable per spec)
- Post-rollout pages checked: 4 (1 passing, 3 errors)
- Legacy pages pending backfill: 21

### Errors

Three pages were created on 2026-04-24 (post-rollout) and are missing `address:` frontmatter. Each must have an address assigned via `./scripts/allocate-address.sh`.

- `wiki/concepts/Persistent Wiki Artifact.md`: created 2026-04-24, no `address:` field.
- `wiki/concepts/Query-Time Retrieval.md`: created 2026-04-24, no `address:` field.
- `wiki/concepts/Source-First Synthesis.md`: created 2026-04-24, no `address:` field.

To fix each: run `./scripts/allocate-address.sh` and add the returned address to the page's frontmatter, then update `.raw/.manifest.json` `address_map`.

### Address-map consistency

- `.raw/.manifest.json` maps `wiki/concepts/DragonScale Memory.md` -> `c-000001`. Frontmatter matches. OK.

### Pending backfill (informational)

21 legacy pages (created before 2026-04-23) have no `address:` field. This is expected; addresses are optional for legacy pages until a backfill pass is run. Full list available by filtering `created: < 2026-04-23` in the vault.

---

## Empty Sections

Four headings have no body content and no sub-headings below them.

- `wiki/concepts/SEO Drift Monitoring.md`: `## Commands` - no content under this heading.
- `wiki/concepts/Search Experience Optimization.md`: `## Command` - no content under this heading.
- `wiki/concepts/Semantic Topic Clustering.md`: `## Command` - no content under this heading.
- `wiki/concepts/cherry-picks.md`: `## Implementation Priority` - section stub, no content.

Suggest: either fill in the command syntax or delete the heading.

---

## Missing Pages

- **E-commerce SEO**: referenced by `[[E-commerce SEO]]` in `wiki/entities/Claude SEO.md`. No dedicated concept or entity page exists. Mentioned in context of SEO workflows. Candidate for a stub concept page.

---

## Cross-Reference Gaps

Entities and concepts mentioned in page bodies without a wikilink. Informational only; safe to auto-fix by wrapping in `[[...]]`.

- `wiki/getting-started.md` mentions `Andrej Karpathy`, `Compounding Knowledge`, and `Hot Cache` in plain text without wikilinks.
- `wiki/overview.md` mentions `cherry-picks`, `claude-obsidian-ecosystem`, and `Wiki vs RAG` in plain text without wikilinks.
- `wiki/sources/claude-obsidian-ecosystem-research.md` mentions `Hot Cache` without a wikilink.
- `wiki/concepts/cherry-picks.md` mentions `Hot Cache` without a wikilink.
- `wiki/comparisons/claude-obsidian-ecosystem.md` mentions `Hot Cache` without a wikilink.

---

## Orphan Pages

None. All non-meta pages have at least one inbound wikilink.

---

## Frontmatter Gaps

None. All scanned pages have `type`, `status`, `created`, `updated`, and `tags` fields.

---

## Stale Index Entries

None. All links in `wiki/index.md` resolve correctly. (`[[Wiki Map]]` resolves to `wiki/Wiki Map.canvas`; `[[concepts/_index]]` etc. resolve to the respective `_index.md` files.)

---

## Semantic Tiling

Skipped. `scripts/tiling-check.py --peek` returned exit 10: ollama not reachable at `http://127.0.0.1:11434`. Start ollama and run `ollama pull nomic-embed-text` to enable.

---

## Dataview Dashboard

See [[dashboard]] for live Dataview queries.

---

## Recommended Fix Order

1. **Address assignment** (3 post-rollout pages) - prevents regression as the vault grows.
2. **Dead link typo** (`[[How does the LLM Wiki pattern work?]]` x5) - one find-and-replace pass across 5 files.
3. **Test placeholder removal** (`[[Foo]]`, `[[notes/Foo]]` x3) - simple deletions.
4. **Empty `## Command(s)` sections** in 3 SEO concept pages - add command examples or remove the heading.
5. **E-commerce SEO stub** - optional, only if the concept is in scope.
6. **Cross-reference gaps** - safe to auto-fix; ask before running.
