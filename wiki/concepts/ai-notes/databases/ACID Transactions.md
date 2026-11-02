---
type: concept
title: "ACID Transactions"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
  - transactions
complexity: intermediate
domain: databases
status: developing
address: c-000308
related:
  - "[[BASE Properties]]"
  - "[[Deadlocks]]"
  - "[[Database Fundamentals]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/Transactions - ACID.md]]"
---

# ACID Transactions

From [[ai-notes|AI-Notes]] (`Transactions - ACID.md`, `SQL/TCL.md`).

A **transaction** is a logical unit of work. Example, a money transfer: read A's balance, debit A, credit B, record the transaction.

## ACID

- **Atomicity**: all or nothing; on error, roll back everything.
- **Consistency**: the database moves from one valid state to another (constraints hold; the total money is unchanged).
- **Isolation**: concurrent transactions don't interfere (no anomalies from interleaving).
- **Durability**: once committed, changes survive crashes.

## Transaction states

Active, then partially committed (changes in the memory buffer), then **committed** (permanent; no rollback possible). Or: active or partially committed, then **failed**, then **aborted** (changes undone). Either way, finally **terminated**.

## TCL (transaction control language)

| Command | Effect |
|---------|--------|
| `SAVEPOINT s` | Mark an intermediate state |
| `ROLLBACK TO s` | Undo back to the savepoint |
| `ROLLBACK` | Undo the whole transaction |
| `COMMIT` | Make the changes permanent (**cannot** roll back afterward) |

Order-processing example: insert order, decrement inventory, charge the account, all inside one transaction so any failure rolls back all three. DBMSs allow many savepoints (implementation limits apply). Isolation levels are set with `SET TRANSACTION ISOLATION LEVEL ...` (read uncommitted, read committed, repeatable read, serializable).

## Schedules and serializability

- **Schedule**: an ordering of operations from concurrent transactions. **Serial** schedules run one transaction at a time; **non-serial** ones interleave.
- A non-serial schedule is **serializable** if its result equals that of some serial order. There are two kinds: **conflict** serializable and view serializable.
- **Conflicting operations** (same item, at least one write): read-write, write-read, write-write.
- **Test**: build a **precedence graph** (nodes are transactions, edges are conflicts). The schedule is conflict-serializable if and only if the graph is **acyclic** (DFS or Kahn's algorithm). Graph algorithms: [[Graph Algorithms]].

Compare the NoSQL alternative, [[BASE Properties]]. Concurrency hazards: [[Deadlocks]].
