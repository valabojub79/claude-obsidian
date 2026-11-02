---
type: concept
title: "Deadlocks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - concurrency
complexity: intermediate
domain: databases
status: developing
address: c-000313
related:
  - "[[ACID Transactions]]"
  - "[[Graph Algorithms]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Deadlocks.md]]"
---

# Deadlocks

Two or more transactions wait **forever**, each holding a resource another needs. From [[ai-notes|AI-Notes]] (an OS concept applied to DBMS transactions; see [[ACID Transactions]]).

T1 locks A and requests B; T2 locks B and requests A. Neither can proceed.

## Four necessary conditions (Coffman), all at once

1. **Mutual exclusion**: a resource is held exclusively.
2. **Hold and wait**: holding one resource while waiting for another.
3. **No preemption**: resources can't be forcibly taken away.
4. **Circular wait**: a cycle of transactions each waiting on the next.

## Handling strategies

| Strategy | Idea |
|----------|------|
| **Prevention** | Break at least one condition (lock ordering breaks circular wait; acquiring all locks up front breaks hold-and-wait) |
| **Avoidance** | **Banker's algorithm**: grant a request only if the system stays in a safe state |
| **Detection and recovery** | Build a **wait-for graph** (an edge Ti to Tj means Ti waits for Tj); detect a **cycle** with DFS or Kahn's algorithm; abort and roll back a victim |
| **Ignorance** ("ostrich") | Do nothing; restart if it happens. Simplest, least robust |

Real DBMSs typically use detection plus victim selection, or lock timeouts (with wait-die and wound-wait schemes as prevention variants). Cycle detection: [[Graph Algorithms]].
