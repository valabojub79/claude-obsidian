---
type: concept
title: "Database Scaling Patterns"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - scaling
  - system-design
complexity: intermediate
domain: databases
status: developing
address: c-000312
related:
  - "[[Partitioning and Sharding]]"
  - "[[Horizontal and Vertical Scaling]]"
  - "[[CAP Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Scaling Patterns.md]]"
---

# Database Scaling Patterns

An incremental playbook as users and data grow. From [[ai-notes|AI-Notes]] (freeCodeCamp "Understanding Database Scaling Patterns").

1. **Query optimization and connection pooling**
   - Index and tune queries; **cache** static or rarely changing data (Redis) instead of hitting the DB.
   - **Connection pool**: reuse open connections rather than opening one per request.
2. **Vertical scaling (scale up)**: a bigger machine (CPU, RAM, SSD). In practice, replicate to the new machine, then switch over. Simple, but capped and costly ([[Horizontal and Vertical Scaling]]).
3. **Command-query responsibility segregation (CQRS)**: separate **writes** (primary, full ACID) from **reads** (replicas; slight lag tolerated). Read replicas absorb read traffic.
4. **Multi-primary replication**: several nodes accept writes and replicate to each other (for example in a ring). Higher write throughput, but conflict resolution is needed.
5. **Partitioning** by function or data ([[Partitioning and Sharding]]).
6. **Horizontal scaling (sharding)** across servers.
7. **Data-center-wise partitioning**: geo-distribute so users hit a nearby region; better latency and disaster recovery.

## Measuring speed

- **Latency**: time per operation (ms or microseconds). Lower is better.
- **Throughput**: operations per second (OPS or TPS).
- **IOPS**: storage I/O operations per second.
- **Bandwidth**: bytes per second moved.

Trade-offs at the distributed end: [[CAP Theorem]], [[BASE Properties]].
