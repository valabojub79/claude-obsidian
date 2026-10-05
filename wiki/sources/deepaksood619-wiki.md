---
type: source
title: "Deepak Sood's Personal Wiki (external mirror)"
source_url: https://github.com/deepaksood619/deepaksood619.github.io
author: "Deepak Sood"
format: knowledge-base-mirror
date_ingested: 2026-10-04
created: 2026-10-04
updated: 2026-10-04
tags:
  - source
  - external-reference
  - computer-science
  - ai
  - databases
  - algorithms
  - economics
  - psychology
status: mirrored
address: c-000124
related:
  - "[[index]]"
sources:
  - "https://github.com/deepaksood619/deepaksood619.github.io"
  - "https://deepaksood619.github.io/"
---

# Deepak Sood's Personal Wiki (external mirror)

A large third-party personal knowledge base, mirrored **as-is** into this vault for
browsing/search convenience. Unlike every other entry in this Sources index, it has
**not** been synthesized into concept/entity pages — at ~2,900 notes it's roughly 20x
the size of this entire vault, so running it through the normal ingest pipeline
(entity/concept extraction, cross-referencing, address assignment per page) doesn't
make sense. Treat it the way you'd treat a vendored dependency: read it, cite it,
pull specific facts into a real wiki page via a normal ingest when something in it
is actually worth synthesizing — but don't assign it DragonScale addresses itself,
and don't expect it to show up in `wiki/index.md`'s page lists.

MIT licensed. Fetched 2026-10-04 as a shallow git clone of the `master` branch (so
it will drift from upstream over time; re-clone to refresh).

## Where it lives

`external/deepak-notes/` at the vault root — a sibling of `wiki/`, not inside it.
Deliberately excluded from this repo's git tracking (see `.gitignore`): it's 235MB
(mostly JPEG screenshots under `media/`), not this user's content to version, and
not auto-staged by the vault's `PostToolUse` commit hook (which only ever adds
`wiki/`, `.raw/`, `.vault-meta/`).

Stripped during the mirror: the upstream repo's own `.obsidian/` config (would
collide with this vault's own Obsidian settings) and its five `CLAUDE.md` files
(Claude Code instructions scoped to *that* repo's Docusaurus build — would be
misleading if loaded from inside this one).

## What's in it (2,923 notes)

| Folder | Notes | Covers |
|---|---|---|
| `ai/` | 238 | ML algorithms, LLMs, computer vision, NLP, deep learning |
| `computer-science/` | 207 | CS fundamentals |
| `technologies/` | 204 | Kafka, Airflow, misc tech |
| `economics/` | 174 | Markets, finance |
| `devops/` | 168 | Kubernetes, CI/CD, infra |
| `knowledge/` | 189 | General reference |
| `languages/` | 131 | Programming languages (Python sub-tree separate, 114 notes) |
| `algorithms/` | 124 | Complexity, searching/sorting, graph theory, DP, strings |
| `education/` | 127 | Learning/education research |
| `mathematics/` | 116 | Math reference |
| `cloud/` | 114 | AWS + other cloud providers |
| `python/` | 114 | Python-specific |
| `devops`, `databases-nosql/` (90), `databases-sql/` (75), `databases/` (35), `data-warehouses/` (76) | — | Split by DB category |
| `book-summaries/` | 96 | — |
| `management/` | 89 | — |
| `frontend/` | 87 | — |
| `networking/` | 83 | — |
| `data-structures/` | 79 | — |
| `about-deepak-sood/` | 78 | Author's own bio/experience — least relevant here |
| `psychology/` | 72 | Overlaps this vault's own Adlerian-psychology notes |
| `decentralized-applications/` | 69 | Crypto/Web3 |
| `courses/` | 52 | Course notes |
| `ideas/` | 35 | Startup/idea research |

## How to use it

It's **not** wikilinked into this vault's graph (its internal links are standard
relative markdown links, e.g. `[Graph Theory](graphtheory/readme.md)` — left
as-is, they resolve fine in Obsidian since Obsidian supports plain markdown links
too, they just won't appear in backlink panes the way `[[wikilinks]]` do).

- Browsing in Obsidian: open any `readme.md` in a topic folder as an entry point —
  every topic folder has one acting as its index.
- Searching from Claude Code: `grep`/`rg` over `external/deepak-notes/`, or just
  ask — a session working in this vault can read it directly.
- Turning something into real wiki content: if a note here is worth building on,
  run it through the normal `wiki-ingest` flow as its own source (cite the
  specific file path under `external/deepak-notes/...` as the source), producing
  a proper addressed concept/entity page cross-linked into this vault — don't
  just copy its prose in wholesale.
