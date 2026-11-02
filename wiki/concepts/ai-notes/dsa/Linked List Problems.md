---
type: concept
title: "Linked List Problems"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - linked-lists
complexity: beginner
domain: programming
status: developing
address: c-000324
related:
  - "[[Data Structures and Algorithms]]"
  - "[[Tree Problems]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Linked List.md]]"
---

# Linked List Problems

From [[ai-notes|AI-Notes]].

| Problem | Approach | Time / Space |
|---------|----------|--------------|
| **Reverse a list** | Three pointers `prev, curr, next`: save next, point `curr->next` to prev, advance | O(n) / O(1) |
| **Detect a cycle** | (1) Set of visited nodes, O(n) space. (2) **Floyd's fast/slow pointers**: they meet if and only if there is a cycle | O(n) / O(1) |
| Remove the n-th node from the end | Length pass, then `len - n - 1` jumps (handle head removal); or a two-pointer gap of n in one pass | O(n) / O(1) |
| **Middle of the list** | (1) Length, then `len/2` jumps. (2) **Tortoise and hare**: fast moves 2, slow moves 1 | O(n) / O(1) |
| Intersection of two lists | (1) Set of list A's nodes. (2) Two pointers that switch heads at the end, meeting at the intersection | O(n+m) / O(1) |
| Remove duplicates (sorted) | If `next.val == curr.val`, unlink next and **don't advance** (the new next may also be a duplicate) | O(n) / O(1) |
| **Palindrome list** | Find the middle, **reverse the second half**, compare with two pointers (optionally restore) | O(n) / O(1) |

## Listed without solutions

Merge two sorted lists; add two numbers; copy a list with random pointers; swap pairs; rotate; reverse in k-groups; sort (merge sort); merge k sorted lists (heap); delete a given node; partition; cycle II (find the start: reset one pointer to the head after meeting); flatten a multilevel doubly linked list; sorted list to BST ([[Tree Problems]]).

Core techniques: dummy head nodes, fast/slow pointers, in-place reversal.
