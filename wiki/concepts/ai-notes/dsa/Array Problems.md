---
type: concept
title: "Array Problems"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - arrays
complexity: beginner
domain: programming
status: developing
address: c-000321
related:
  - "[[Data Structures and Algorithms]]"
  - "[[String Problems]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/Arrays.md]]"
---

# Array Problems

From [[ai-notes|AI-Notes]] (Coding Ninjas list). The approaches the source works out:

| Problem | Approach | Time / Space |
|---------|----------|--------------|
| First and last occurrence in a **sorted** array | Linear scan updating last (better: two **binary searches**, `O(log n)`) | O(n) / O(1) |
| Find a duplicate | (1) Hash set, stop on the first repeat. (2) Sort, then compare neighbors | O(n) / O(n); O(n log n) / O(1) |
| Element appearing once (others twice) | Frequency map (or **XOR all**, which is O(1) space) | O(n) / O(n) |
| Pair with target sum | (1) Double loop O(n^2). (2) **Hash map** of seen values. (3) **Two pointers** on a sorted array: move start or end by comparing the sum | O(n) / O(1) for two pointers |
| Triplet with sum | Triple loop O(n^3) (better: sort plus two pointers, O(n^2)) | |
| Max-sum subarray of size k | **Fixed sliding window**: add the incoming element, drop the outgoing one | O(n) / O(1) |
| Smallest subarray with sum >= target | All subarrays O(n^2); better a **variable sliding window** (shrink while the sum is at least the target), O(n) | |

(The source lists the sort-based duplicate approach as O(n) time; sorting makes it O(n log n).)

## Listed without solutions

Implement the sorting algorithms; sort 0s, 1s and 2s (Dutch national flag); remove duplicates from a sorted array; prefix sums and range sums; **Kadane's** max subarray; all subarrays or subsequences; subsequence check; rotate by k (three reversals); negatives before positives; move zeros to the end; rotate a matrix 90 degrees (transpose plus reverse rows); diagonal sum; max-sum submatrix (Kadane in 2D).

Related: [[String Problems]] (sliding window on strings).
