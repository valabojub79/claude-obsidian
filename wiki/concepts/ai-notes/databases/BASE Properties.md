---
type: concept
title: "BASE Properties"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - distributed-systems
complexity: intermediate
domain: databases
status: developing
address: c-000309
related:
  - "[[ACID Transactions]]"
  - "[[CAP Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Base Properties.md]]"
---

# BASE Properties

The availability-first counterpart to [[ACID Transactions|ACID]], typical of distributed NoSQL stores. From [[ai-notes|AI-Notes]].

- **Basically Available**: always accepts reads and writes, even if some aren't immediately consistent (a shop stays responsive).
- **Soft state**: state may change over time without new input, as replicas sync (inventory counts updated asynchronously).
- **Eventually consistent**: given time without new writes, all replicas converge (a profile update propagates).

## ACID or BASE?

| Choose ACID when | Choose BASE when |
|------------------|------------------|
| Integrity is critical (banking, payments) | Availability and scale are critical (social feeds, content) |
| Strict transactional control is needed | Data is spread across many nodes (horizontal scaling) |
| Single node or tightly coupled clusters | Real-time responsiveness matters and staleness is tolerable |

Theory behind the trade-off: [[CAP Theorem]].
