---
type: concept
title: "SQL Window Functions"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - sql
  - analytics
complexity: intermediate
domain: databases
status: developing
address: c-000320
related:
  - "[[SQL Overview]]"
  - "[[SQL Case Study - Shark Tank India]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/SQL/Window Functions.md]]"
---

# SQL Window Functions

**Analytical** functions computed over a "window" of related rows **without collapsing them** (unlike `GROUP BY`). From [[ai-notes|AI-Notes]] (CampusX; machinelearningplus exercises).

```sql
fn(...) OVER (PARTITION BY grp ORDER BY col [frame])
```

## The functions

- **Ranking**: `ROW_NUMBER`, `RANK`, `DENSE_RANK` (also `NTILE`, `PERCENT_RANK`).
- **Value**: `FIRST_VALUE`, `LAST_VALUE`, `NTH_VALUE`, **`LAG`** (previous row), **`LEAD`** (next row).
- **Aggregates as windows**: `SUM`, `AVG`, `MIN`, `MAX`, `COUNT`.

## Ranks compared (scores 100, 90, 90, 80)

| Function | Result | Note |
|----------|--------|------|
| `ROW_NUMBER` | 1, 2, 3, 4 | Unique, arbitrary among ties; a temporary key |
| `RANK` | 1, 2, 2, **4** | Gaps after ties |
| `DENSE_RANK` | 1, 2, 2, **3** | No gaps |

## Frames (a window within the window)

- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: **running total**.
- `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`: the whole partition (needed for a correct `LAST_VALUE`).
- `ROWS BETWEEN 2 PRECEDING AND 1 FOLLOWING`: a sliding window.

**Moving average** smooths fluctuations to reveal trend, a staple of time series: `AVG(sales) OVER (ORDER BY day ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)`.

Classic pattern, **top-1 per group**: `ROW_NUMBER() OVER (PARTITION BY industry ORDER BY amount DESC)` in a subquery, then `WHERE rn = 1` (see [[SQL Case Study - Shark Tank India]]).
