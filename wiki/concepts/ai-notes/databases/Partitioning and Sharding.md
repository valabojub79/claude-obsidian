---
type: concept
title: "Partitioning and Sharding"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - scaling
complexity: intermediate
domain: databases
status: developing
address: c-000315
related:
  - "[[Database Scaling Patterns]]"
  - "[[CAP Theorem]]"
  - "[[Horizontal and Vertical Scaling]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Partitioning and Sharding.md]]"
---

# Partitioning and Sharding

Split data so queries touch less of it and load spreads out, which improves performance and defers costly scaling. From [[ai-notes|AI-Notes]] (Love Babbar, Ankit Bhayani).

## Partitioning (within one database server)

- **Horizontal**: split **rows** (by date range, region, hash).
- **Vertical**: split **columns** (hot columns vs large or rarely used ones).

Several partitions can live on the same machine; the database prunes partitions that a query doesn't need.

## Sharding (across machines)

A form of horizontal partitioning in which row subsets (**shards**) live on **different database instances or servers**. A shard key (user_id, region) routes each query.

- Pros: horizontal scale for storage and write throughput; fault isolation.
- **Cons**: queries spanning shards (joins, aggregates) are complex and slow; rebalancing ("resharding") is painful; hot shards appear with skewed keys; cross-shard transactions are hard ([[CAP Theorem]]).

Choose shard keys with high cardinality and even access. Consistent hashing eases rebalancing.

Where it fits in the overall progression: [[Database Scaling Patterns]].
