---
type: concept
title: "Database Fundamentals"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - databases
  - databases
complexity: beginner
domain: databases
status: developing
address: c-000311
related:
  - "[[ACID Transactions]]"
  - "[[Normalization]]"
  - "[[SQL Overview]]"
  - "[[CAP Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/Database Management System/Database Core concepts/RDBMS.md]]"
---

# Database Fundamentals

From [[ai-notes|AI-Notes]] (Love Babbar's DBMS playlist; placement-oriented).

- **Data** = raw facts (scraped HTML with tags); **information** = processed, meaningful data.
- **Database** = data stored electronically; **DBMS** = software between users or applications and the data (storage, querying, concurrency, security, recovery).

## Kinds of databases

| Kind | Examples |
|------|----------|
| Relational (SQL) | MySQL, PostgreSQL, Oracle |
| Document (NoSQL) | MongoDB |
| Graph | Neo4j |
| **Vector** | Pinecone, Weaviate (for [[RAG Architecture\|RAG]]) |
| Key-value cache | Redis |

## Concepts

- **Instance**: the database's state at a moment. **Schema**: its logical structure (entities, relationships, constraints).
- **Abstraction levels**: physical (storage), logical (schema), view (what each user sees).
- **Languages**: DDL, DML, DCL, TCL (see [[ACID Transactions]]), DQL.
- **App connectivity**: SQLAlchemy (Python), JDBC (Java), ODBC (C/C++).
- **Architectures**: 1-tier (all on one machine); 2-tier (client plus DB server); 3-tier (client, **application server**, DB), which adds a business-logic layer for security and scalability. See [[Client-Server Architecture]].
- **Entities**: **strong** (independently identifiable, like Student) vs **weak** (dependent, like CourseEnrollment). The ER model links them via relationships (1:1, 1:N, M:N).

> [!gap] Unanswered in source
> File system vs DBMS, the data-model list, database languages in detail, ER relationship types and attribute types are questions without answers. ER, Data Models and Indexing pages are title-only stubs.

## Database pages

[[ACID Transactions]] · [[BASE Properties]] · [[CAP Theorem]] · [[Deadlocks]] · [[Normalization]] · [[Partitioning and Sharding]] · [[Database Scaling Patterns]] · [[SQL Overview]]
