---
type: concept
title: "Graph Algorithms"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - graphs
complexity: intermediate
domain: programming
status: developing
address: c-000323
related:
  - "[[Data Structures and Algorithms]]"
  - "[[Deadlocks]]"
  - "[[ACID Transactions]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Graph.md]]"
---

# Graph Algorithms

From [[ai-notes|AI-Notes]] (`Graph.md`): a topic plan of **traversal, BFS, DFS, shortest paths, connectivity**, with one worked problem.

## Worked: path from a source node to a destination

DFS: mark the node visited; for each unvisited neighbor, return true if it is the destination or if the recursive call finds a path; otherwise return false. **O(V + E)** time; O(V) visited set plus recursion stack.

## Core toolkit (standard)

| Need | Algorithm |
|------|-----------|
| Reachability, components | BFS or DFS, O(V + E); union-find |
| Shortest path, unweighted | BFS |
| Shortest path, non-negative weights | **Dijkstra** (heap), O(E log V) |
| Negative weights | Bellman-Ford |
| All pairs | Floyd-Warshall |
| **Directed cycle detection** | DFS with a recursion stack (gray/black colors), or **Kahn's topological sort** (a cycle exists if not all nodes are output) |
| Ordering with dependencies | Topological sort |
| Minimum spanning tree | Kruskal, Prim |

Directed-cycle detection appears twice in the database notes: the **wait-for graph** for [[Deadlocks]] and the **precedence graph** for conflict serializability in [[ACID Transactions]]. Graph ideas also underlie [[Hierarchical Clustering]] (single linkage is essentially a minimum spanning tree).
