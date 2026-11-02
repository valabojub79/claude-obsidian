---
type: concept
title: "SQL Overview"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - sql
  - databases
complexity: beginner
domain: databases
status: developing
address: c-000318
related:
  - "[[SQL Window Functions]]"
  - "[[SQL Views]]"
  - "[[SQL Joins]]"
  - "[[SQL Case Study - Shark Tank India]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/SQL/SQL.md]]"
---

# SQL Overview

Hub page for [[ai-notes|AI-Notes]]' SQL section. Many listed sub-pages (commands, datatypes, constraints, operators, clauses, filtering, aggregates, order of execution, CTEs, built-in functions, stored procedures) are **empty in the source**; the ones with content are summarized here or linked.

## Logical order of execution

`FROM / JOIN`, then `WHERE`, `GROUP BY`, `HAVING`, `SELECT` (window functions here), `DISTINCT`, `ORDER BY`, `LIMIT`. This is why `WHERE` can't use `SELECT` aliases but `ORDER BY` can. The source's ORDER BY example shows the same flow: `FROM`, `WHERE class = 12`, `SELECT *`, `ORDER BY id`.

## ORDER BY

Sort ascending (default) or descending; multiple columns; by column **position** (`ORDER BY 2`); by **expressions** (`ORDER BY CASE ... END`). Sorting costs `O(n log n)`; databases use external merge sort for large data, or avoid sorting entirely via indexes.

## CASE

Row-level IF/THEN logic:

```sql
SELECT name,
       CASE WHEN state = 'CA' THEN 'yes' ELSE 'no' END AS is_california
FROM players;
```

Any number of `WHEN` branches; the `END AS` alias becomes a new column. Combine with aggregates for **conditional counts**: `SUM(CASE WHEN ... THEN 1 ELSE 0 END)`.

## Subqueries

A query inside a query.

- **By result shape**: **scalar** (one value), **row** (one row, many columns), **column** (many rows, one column, used with `IN`), **table** (many rows and columns, used in `FROM`).
- **By dependence**: **independent** (inner runs once) vs **correlated** (inner references the outer row and runs per row, so it's often slower; rewrite as a join or window function).

## More pages

[[SQL Joins]] · [[SQL Window Functions]] · [[SQL Views]] · [[ACID Transactions]] (TCL) · [[Normalization]] · case study: [[SQL Case Study - Shark Tank India]]. Scenario-based practice: TestGorilla's SQL interview questions.
