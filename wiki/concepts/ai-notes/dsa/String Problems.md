---
type: concept
title: "String Problems"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - programming
  - dsa
  - strings
complexity: intermediate
domain: programming
status: developing
address: c-000326
related:
  - "[[Data Structures and Algorithms]]"
  - "[[Array Problems]]"
sources:
  - "[[.raw/repos/AI-Notes/Data Structures And Algorithms/String.md]]"
---

# String Problems

Merged from [[ai-notes|AI-Notes]]' `String.md` and its subfolder (Anagrams and Grouping, Substrings and Subsequence, String Operations, and tiny stubs for Pattern Matching, Searching and Indexing, Segmentation and Validation, Transformation and Distance).

## Worked approaches

| Problem | Approach | Complexity |
|---------|----------|-----------|
| Reverse a string | Two pointers swapping inward | O(n) / O(1) |
| Valid palindrome (alphanumeric only) | Filter, then two pointers; better, skip non-alphanumerics in place | O(n) / O(1) |
| Are two strings anagrams? | (1) Sort both and compare, O(n log n). (2) **26-count array**: +1 for s1, -1 for s2, all zero at the end | O(n) / O(26) |
| Find all anagram substrings | Brute: every window of length m, sort and compare; better a **sliding window with counts**, O(n) | |
| Group anagrams | Hash map keyed by the sorted string (or a count tuple) | O(n k log k) |
| Longest common subsequence | Brute: all subsequences, O(2^n + 2^m); proper: **DP** O(nm) | |
| Longest palindromic substring | Brute: all substrings, O(n^2) or more; better **expand around center** O(n^2) / O(1), or Manacher O(n) | |
| Longest common substring | Brute O(n^2) comparisons; DP O(nm) | |
| Count palindromic substrings | Generate and check, or expand around centers | |
| Longest substring without repeats | **Sliding window plus last-seen map** | O(n) |

(The source's "longest substring without repeating characters" body is a copy-paste of the palindrome steps; use a sliding window.)

## Listed without solutions

String compression; first non-repeating character; KMP and Rabin-Karp; `atoi`; longest common prefix; count-and-say; permutations; word break (DP); valid parentheses (stack); edit distance (DP); minimum window substring; zigzag conversion; wildcard and regex matching (DP); multiply strings; `strStr`; valid palindrome II; longest substring with at most K distinct characters.

Anagram definition: same length and the same character frequencies.
