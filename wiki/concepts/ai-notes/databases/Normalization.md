---
type: concept
title: "Normalization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - schema-design
complexity: intermediate
domain: databases
status: developing
address: c-000314
related:
  - "[[Database Fundamentals]]"
  - "[[SQL Joins]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Normalization.md]]"
---

# Database Normalization

Split large tables into smaller related ones to remove **redundancy**, which wastes storage and causes **insertion, update and deletion anomalies**. From [[ai-notes|AI-Notes]] (Love Babbar).

## Functional dependencies (Armstrong's axioms)

`A -> B`: A's value determines B's.

- **Reflexive**: if B is a subset of A, then `A -> B`.
- **Augmentation**: if `A -> B`, then `AX -> BX`.
- **Transitive**: if `A -> B` and `B -> C`, then `A -> C`.

## Normal forms

| Form | Requirement |
|------|-------------|
| **1NF** | Every attribute holds **atomic** values (no lists or repeating groups) |
| **2NF** | 1NF plus **no partial dependency**: non-key attributes depend on the *whole* composite key, not part of it |
| **3NF** | 2NF plus **no transitive dependency**: non-key attributes depend only on the key, not on other non-key attributes |
| **BCNF** | 3NF plus for every FD `X -> Y`, **X is a superkey** |

## Denormalization

Deliberately re-introduce redundancy (merge tables, precompute aggregates) to speed up **read-heavy** workloads and avoid expensive joins: analytics warehouses, star schemas, caches. The trade-off is update cost and integrity risk.

Normalized data is then recombined with [[SQL Joins|joins]].
