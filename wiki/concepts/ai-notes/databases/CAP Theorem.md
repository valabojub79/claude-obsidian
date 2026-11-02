---
type: concept
title: "CAP Theorem"
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
address: c-000310
related:
  - "[[BASE Properties]]"
  - "[[Partitioning and Sharding]]"
  - "[[Horizontal and Vertical Scaling]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/CAP theorem.md]]"
---

# CAP Theorem

For a **distributed** data system (multiple connected database servers), you can guarantee at most **two of three** at the same time. From [[ai-notes|AI-Notes]] (Love Babbar; AlgoMaster blog).

- **Consistency**: every read sees the latest write (all nodes agree).
- **Availability**: every request gets a (non-error) response.
- **Partition tolerance**: the system keeps working when the network splits into groups that can't communicate.

## System types

| Type | During a partition | Examples |
|------|-------------------|----------|
| **CP** | Refuses or blocks requests on inconsistent nodes; consistent but less available | HBase, MongoDB (default config), ZooKeeper |
| **AP** | Serves possibly stale data; reconciles later (eventual consistency, see [[BASE Properties]]) | Cassandra, DynamoDB, CouchDB |
| **CA** | Can't tolerate partitions | Single-node RDBMS |

> [!note] Practical reading
> In real networks partitions *will* happen, so a distributed system effectively chooses **CP or AP** while partitioned. "CA" describes non-distributed (single-site) systems. PACELC extends CAP: **e**lse (no partition), trade **l**atency against **c**onsistency.

Scaling context: [[Partitioning and Sharding]], [[Database Scaling Patterns]].
