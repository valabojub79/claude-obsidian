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

Last updated: 2026-06-06 | Total pages: 71 | Sources ingested: 9

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

---

## Entities

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

---

## Sources

- [[nvme-base-spec-2.3]] — 2026-05-22 | NVMe Base Spec Rev 2.3 (784pp) | 6 wiki pages created
- [[courage-to-be-disliked]] — 2026-05-21 | Koga + Kishimi (Hinglish) | 9 wiki pages created
- [[claude-obsidian-ecosystem-research]] — 2026-04-08 | web research across 16+ repos | 8 wiki pages created

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
