---
type: concept
title: "SQL Views"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - sql
complexity: beginner
domain: databases
status: developing
address: c-000319
related:
  - "[[SQL Overview]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/SQL/Views.md]]"
---

# SQL Views

A **view** is a virtual table defined by a stored query. From [[ai-notes|AI-Notes]].

**Why**: (1) **access control**, exposing only certain columns or rows to a user; (2) **reuse**, encapsulating a complex query behind a simple name.

## Types

| Type | Definition |
|------|-----------|
| Simple | One table, no `GROUP BY` |
| Complex | Joins, aggregation, `GROUP BY` |
| Inline | A subquery in `FROM` (a temporary, unnamed "view") |
| **Materialized** | Stores the query's **result physically**; fast reads, but must be **refreshed** and can be stale (PostgreSQL, Oracle; MySQL lacks native support) |

```sql
CREATE VIEW active_customers AS
SELECT id, name, email FROM customers WHERE status = 'active';
DROP VIEW active_customers;
```

## Can you UPDATE or DELETE through a view?

Only through **updatable** views, which typically require a **single base table**, no aggregation or `GROUP BY`/`DISTINCT`, and no computed or derived columns. Otherwise the view is read-only (or needs `INSTEAD OF` triggers).
