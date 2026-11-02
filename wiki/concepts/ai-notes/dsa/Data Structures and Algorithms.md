---
type: concept
title: "Data Structures and Algorithms"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - interview
complexity: beginner
domain: programming
status: developing
address: c-000322
related:
  - "[[Array Problems]]"
  - "[[String Problems]]"
  - "[[Linked List Problems]]"
  - "[[Stack and Monotonic Stack Problems]]"
  - "[[Tree Problems]]"
  - "[[Graph Algorithms]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Arrays.md]]"
---

# Data Structures and Algorithms

Hub page for [[ai-notes|AI-Notes]]' DSA section: interview problem lists (Coding Ninjas / Naukri Code360) with approach notes and complexity, coded in C++.

| Topic | Page | Coverage in the source |
|-------|------|------------------------|
| Arrays | [[Array Problems]] | Good: two pointers, sliding window, hashing |
| Strings | [[String Problems]] | Problem list plus anagram and substring approaches |
| Linked lists | [[Linked List Problems]] | Good: fast/slow pointers, reversal |
| Stack / monotonic stack | [[Stack and Monotonic Stack Problems]] | Next greater element, temperatures, rainwater |
| Trees and BST | [[Tree Problems]] | Traversals, views, BST operations, a 22-question list |
| Graphs | [[Graph Algorithms]] | One DFS problem plus a topic plan |
| Heap, Recursion/DP, Stack-Queue (conversion, implementation) | none | **Empty** in the source |

## Recurring patterns

1. **Brute force first** (nested loops, generate all substrings), then optimize.
2. **Hashing** (set or map) trades `O(n)` space for `O(n)` time.
3. **Two pointers** on sorted data, and fast/slow pointers on lists.
4. **Sliding window** for fixed or variable-length subarrays and substrings.
5. **Monotonic stack** for "next greater or smaller".
6. **Recursion on trees**; BFS for levels and views.

Graph-cycle detection also underpins DBMS theory: [[Deadlocks]] (wait-for graph) and [[ACID Transactions]] (precedence graph).
