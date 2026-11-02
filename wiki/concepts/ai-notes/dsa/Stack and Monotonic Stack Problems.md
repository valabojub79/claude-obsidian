---
type: concept
title: "Stack and Monotonic Stack Problems"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - stacks
complexity: intermediate
domain: programming
status: developing
address: c-000325
related:
  - "[[Data Structures and Algorithms]]"
  - "[[Array Problems]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Stack/Monotonic Problems.md]]"
---

# Stack and Monotonic Stack Problems

From [[ai-notes|AI-Notes]] (`Stack/Monotonic Problems.md`; the conversion and implementation pages are empty).

A **monotonic stack** keeps elements in increasing (or decreasing) order, popping anything that violates the order. Each element is pushed and popped at most once, so the total is O(n).

| Problem | Approach | Time / Space |
|---------|----------|--------------|
| **Next greater element (circular)** | Brute: conceptually double the array, two loops, O(n^2). **Stack**: iterate from the back over `2n` indices (`i % n`); pop while `top <= a[i]`; the answer is the top or -1; push `a[i]` | O(n) / O(n) |
| **Daily temperatures** | Iterate from the end with a stack of (index, temp); pop cooler or equal days; answer = `top.index - i` | O(n) / O(n) |
| **Trapping rainwater** | For each bar: `min(maxLeft, maxRight) - height` (prefix and suffix max arrays; or a stack, or two pointers with O(1) space) | O(n) / O(n) |

Variants: next smaller, previous greater or smaller, stock span.

Listed without solutions: **largest rectangle in histogram** (previous and next smaller via monotonic stack, O(n)) and **maximal rectangle** (histogram per row of a binary matrix).
