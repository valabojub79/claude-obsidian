---
type: concept
title: "SQL Joins"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - sql
complexity: beginner
domain: databases
status: seed
address: c-000317
related:
  - "[[SQL Overview]]"
  - "[[Normalization]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/SQL/Joins.md]]"
---

# SQL Joins

Normalized data is spread across tables ([[Normalization]]); **joins** recombine it on related keys. From [[ai-notes|AI-Notes]], where the page sets up `orders`, `customers` and `salesman` practice tables but leaves the explanations empty.

| Join | Returns |
|------|---------|
| `INNER JOIN` | Only matching rows from both tables |
| `LEFT JOIN` | All left rows, plus matches (NULL if none) |
| `RIGHT JOIN` | All right rows, plus matches |
| `FULL OUTER JOIN` | All rows from both (MySQL emulates it with a UNION of left and right joins) |
| `CROSS JOIN` | Cartesian product |
| Self join | A table joined to itself (employee and manager) |

Anti-join pattern: `LEFT JOIN ... WHERE right.key IS NULL` finds rows with no match. Practice: the Medium "SQL joins practice" set linked in the source.
