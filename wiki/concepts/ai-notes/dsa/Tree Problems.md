---
type: concept
title: "Tree Problems"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - trees
complexity: intermediate
domain: programming
status: developing
address: c-000327
related:
  - "[[Data Structures and Algorithms]]"
  - "[[Graph Algorithms]]"
  - "[[Decision Tree]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Tree/Questions.md]]"
---

# Tree Problems

From [[ai-notes|AI-Notes]] (`Tree/Traversals.md`, `Tree/Views of Tree.md`, `Tree/Binary Search Tree/Problems.md`, `Tree/Questions.md`).

## Traversals

- **DFS** (recursive): inorder (L, N, R; gives **sorted** order for a BST), preorder (N, L, R), postorder (L, R, N).
- **Level order (BFS)** with a queue.

## Views (BFS plus bookkeeping)

- **Left / right view**: first or last node at each level.
- **Top / bottom view**: track the horizontal distance `hd` (root 0, left -1, right +1); keep the first (top) or last (bottom) node seen per `hd`, ordered by `hd`.

## Binary search tree operations

| Operation | Approach | Complexity |
|-----------|----------|-----------|
| Search | Go left if the target is smaller, right if larger | O(h): O(log n) if balanced, O(n) if skewed |
| Minimum / maximum | Leftmost / rightmost node | O(h) |
| **Ceil** / floor | Walk down, recording the best candidate | O(h) |
| Insert | Walk to a null child and attach | O(h) |
| Delete | 0 or 1 child: splice it out. 2 children: replace with the inorder successor (leftmost of the right subtree) | O(h) |
| Is it a BST? | Inorder traversal is strictly increasing; or recurse with (min, max) bounds | O(n) |

(The source writes O(log n) for search and O(n) for min and insert; all are O(h).)

## Question list (22, mostly unsolved in the source)

Max depth; balanced check; BST check; LCA; diameter; sorted array to balanced BST; tree to doubly linked list; serialize and deserialize; identical trees; symmetric tree; kth smallest or largest in a BST; max path sum; build from inorder plus preorder or postorder; boundary traversal; subtree check; root-to-leaf paths; vertical order; sum tree; path sum; height-balanced; flatten to a linked list.

Machine-learning trees are a different structure: [[Decision Tree]].
