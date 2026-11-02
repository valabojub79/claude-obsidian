---
type: source
title: "Associative Long Short-Term Memory"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1602.03032"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - memory
status: ingested
address: c-000220
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
  - "[[Neural Turing Machines]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/associative-lstm.md]]"
---

# Associative Long Short-Term Memory

[Paper](http://arxiv.org/abs/1602.03032) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Augment LSTMs with an external key-value memory based on **Holographic Reduced Representations** (Plate 2003). Lookups are complex-valued multiplications with no extra parameters; keeping several redundant memory copies reduces retrieval noise. It beats LSTMs and unitary variants on copying and memorization tasks.

## Key points

- LSTM limits: N cells need NxN weights, and there's no way to index memory.
- More memory copies mean less noisy retrieval.
- Tasks: episodic copy, XML modeling, variable assignment, arithmetic, sequence prediction.

## Critique (Denny Britz)

NTMs get only a brief appendix comparison (and are probably simpler and better); no comparison to attention or memory networks. Deep vanilla LSTMs do surprisingly well, so is the complexity worth it?
