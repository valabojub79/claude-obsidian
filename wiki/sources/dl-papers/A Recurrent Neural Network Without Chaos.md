---
type: source
title: "A Recurrent Neural Network Without Chaos"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1612.06212"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - dynamical-systems
status: ingested
address: c-000211
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
  - "[[Gated Recurrent Unit]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/rnn_no_chaos.md]]"
---

# A Recurrent Neural Network Without Chaos

[Paper](https://arxiv.org/abs/1612.06212) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Laurent and von Brecht propose the **Chaos-Free Network (CFN)**, a gated RNN much simpler than LSTM or GRU whose dynamics are provably non-chaotic and interpretable, yet it nearly matches LSTM on language modeling.

## Key points

- Without input, LSTM and GRU are **chaotic**: perturbing the initial state by `1e-7` gives wildly different trajectories. With input they're externally driven and converge, but remain hard to interpret.
- With no input, the CFN state simply **decays to 0**; higher layers decay more slowly (layer 1 retains about 10 to 20 steps, layer 2 about 100).
- PTB with dropout: 2-layer LSTM 71.8 vs **CFN 72.2**. Text8 without dropout: 139.9 vs 142.0. The CFN has the parameters of a 1-layer LSTM.
- Conclusion: LSTMs don't owe their performance to chaotic dynamics.

## Critique (Denny Britz)

An excellent, accessible introduction to dynamical systems. The slower decay in higher layers might model long-range dependencies efficiently. Practical value is mainly interpretability, since real RNNs are almost always input-driven.
