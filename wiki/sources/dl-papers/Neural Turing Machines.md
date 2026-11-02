---
type: source
title: "Neural Turing Machines"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1410.5401"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - memory
  - attention
  - algorithmic
status: ingested
address: c-000271
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[End-To-End Memory Networks]]"
  - "[[Learning to Execute]]"
  - "[[Associative Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/neural-turing-machines.md]]"
---

# Neural Turing Machines

[Paper](http://arxiv.org/abs/1410.5401) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Graves, Wayne and Danihelka couple a controller network (LSTM or MLP) with an external **memory matrix** accessed by differentiable read and write heads. Heads use soft attention combining **content-based** addressing (similarity) and **location-based** addressing (shifts). Trained end to end, NTMs learn algorithms such as copy, repeat copy, associative recall, n-gram modeling and priority sort, and generalize to longer sequences than LSTMs.

## Key points

- Whether an LSTM or MLP controller is better depends on the task; the LSTM's own "cache" can become a bottleneck.
- Hyperparameters: controller size, number of heads, memory size.
- Addressing traces show learned, interpretable "programs".
- Parameters don't grow quadratically with memory, unlike LSTM hidden size.
- Toy-scale tasks (sequences of 8-bit vectors).

## Critique (Denny Britz)

At what length do NTMs break down? Could fuzzy NTM programs be converted to deterministic ones?

## Connections

Successor: the Differentiable Neural Computer. The read/write attention foreshadows Transformers' key-value attention.
