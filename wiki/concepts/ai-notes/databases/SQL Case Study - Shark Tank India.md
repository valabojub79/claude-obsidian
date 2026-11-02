---
type: concept
title: "SQL Case Study - Shark Tank India"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - sql
  - case-study
complexity: intermediate
domain: databases
status: developing
address: c-000316
related:
  - "[[SQL Window Functions]]"
  - "[[SQL Overview]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Case Studies/Shark Tank India/Solutions.md]]"
---

# SQL Case Study: Shark Tank India

[[ai-notes|AI-Notes]]' worked SQL case study on a Shark Tank India dataset (pitches, industries, deals, sharks, seasons). The other case studies listed (Data Science Jobs, Google Play Store, Indian Tourism, Swiggy) have empty solution files.

## Problems and approaches

1. **Highest funding per industry (domain)**, to promote season 4:
   - **Approach A**: `ROW_NUMBER() OVER (PARTITION BY industry ORDER BY total_deal_amount DESC)` in a subquery, then keep `rn = 1`. `ROW_NUMBER` rather than `DENSE_RANK`, because the data has ties and only one row per industry is wanted.
   - **Approach B**: `GROUP BY industry` with `MAX(total_deal_amount)` (gives the amount, not the full row).
2. **Industries where the female-to-male pitcher ratio exceeds 70%**: an inner query sums female and male pitchers per industry (keeping industries with at least one of each); the outer query computes the ratio and filters.
3. **Per season**: total pitches, pitches with offers, converted pitches, and conversion percentages (conditional `SUM(CASE ...)`).
4. Season with the **highest average monthly sales**, and the top industries in it.
5. Industries with **consistently increasing funds** across seasons (`LAG` comparisons).
6. A **payback-period calculator**: given a startup, years to recoup the shark's investment from its revenue.
7. Which shark invests the **most per deal on average**.
8. A **stored procedure**: input season and shark name; output that shark's total investment by industry.
9. The most **diversified** shark (distinct industries invested in).
10. Concept question: **indexes in MySQL**. B-tree indexes speed up lookups, joins and sorts at the cost of write overhead and storage. Index columns that are selective and used in `WHERE`, `JOIN` and `ORDER BY`; avoid indexing low-cardinality or frequently updated columns.

Techniques used: [[SQL Window Functions]], subqueries and CASE ([[SQL Overview]]), stored procedures.
