---
type: source
title: "Pointer Networks"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.03134"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - attention
  - combinatorial-optimization
status: ingested
address: c-000276
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Incorporating Copying Mechanism in Sequence-to-Sequence Learning]]"
  - "[[Pointer Sentinel Mixture Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/pointer-networks.md]]"
---

# Pointer Networks

[Paper](http://arxiv.org/abs/1506.03134) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Vinyals, Fortunato and Jaitly's **Ptr-Net**: a seq2seq model whose outputs are **positions in the input**. The attention distribution itself is the output (a soft "pointer") instead of being used to blend encoder states. The output vocabulary scales with input length. Learns approximate solutions to **convex hull**, **Delaunay triangulation** and **TSP**.

## Key points

- `O(n^2)` attention; a minor modification of standard attention.
- Outputting coordinates with plain seq2seq would ignore output constraints and be less efficient.
- 512-unit LSTM, SGD lr 1.0, batch 128, gradient clipping 2.0.
- On TSP the student **beats its teacher** (the approximate solver that generated labels).

## Critique (Denny Britz)

Could it generate labeled spans (pointer plus class) for tagging, as in [[Multilingual Language Processing From Bytes]]?

## Connections

Copy mechanisms ([[Incorporating Copying Mechanism in Sequence-to-Sequence Learning|CopyNet]], pointer-generator), [[Pointer Sentinel Mixture Models]], extractive QA span pointers, neural combinatorial optimization.
