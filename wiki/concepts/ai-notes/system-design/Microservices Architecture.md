---
type: concept
title: "Microservices Architecture"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - system-design
  - system-design
complexity: beginner
domain: system-design
status: seed
address: c-000400
related:
  - "[[Client-Server Architecture]]"
  - "[[Horizontal and Vertical Scaling]]"
sources:
  - "[[.raw/repos/AI-Notes/System Design/Microservices Architecture.md]]"
---

# Microservices Architecture

[[ai-notes|AI-Notes]] lists only resources here: a microservices interview-questions video and Arpit Bhayani's microservices playlist.

In brief: split an application into small, **independently deployable** services, each owning its data and talking over APIs or messaging. Benefits: independent scaling and deployment, team autonomy, fault isolation. Costs: network latency and failures, distributed transactions and data consistency, observability, operational overhead. Start with a well-structured monolith and split when boundaries and scale demand it.

> [!gap] Source stub
> Only resource links in the source.
