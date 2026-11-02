---
type: concept
title: "Horizontal and Vertical Scaling"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - system-design
  - system-design
  - scaling
complexity: beginner
domain: system-design
status: developing
address: c-000399
related:
  - "[[Database Scaling Patterns]]"
  - "[[Partitioning and Sharding]]"
  - "[[CAP Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/System Design/Horizontal and Vertical Scaling.md]]"
---

# Horizontal and Vertical Scaling

When a growing user base raises latency and lowers throughput, scale up or scale out. From [[ai-notes|AI-Notes]] (AlgoMaster).

| | Vertical (scale up) | Horizontal (scale out) |
|-|--------------------|-----------------------|
| How | A bigger machine (more CPU, RAM, disk) | More machines behind a **load balancer** |
| Pros | Simple; no architecture changes, so it's the preferred **first step** | Near-unlimited scale; **fault tolerance** |
| Cons | **Hard ceiling**; a **single point of failure** | Complexity: data consistency, load balancing, inter-node communication, distributed state ([[CAP Theorem]]) |

For databases specifically, see [[Database Scaling Patterns]] and [[Partitioning and Sharding]]. Stateless app servers scale out easily; stateful data tiers are the hard part.
