---
type: source
title: "Adaptive Computation Time for Recurrent Neural Networks"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1603.08983"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - conditional-computation
status: ingested
address: c-000216
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Recurrent Neural Networks]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/act-rnn.md]]"
---

# Adaptive Computation Time for Recurrent Neural Networks

[Paper](http://arxiv.org/abs/1603.08983) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Graves' Adaptive Computation Time (ACT) lets an RNN decide how many internal steps ("pondering") to spend on each input. A sigmoid halting unit accumulates probability until it reaches 1; outputs and states are the halting-weighted mean of the intermediate steps. A **ponder cost** term in the loss penalizes excess computation and stops it from computing forever.

## Key points

- Fully differentiable; works with any RNN cell (LSTM included).
- The model learns to ponder more on hard inputs (parity, logic, addition, sorting); on character-level Wikipedia it ponders more at word and sentence boundaries.
- The ponder-cost weight is a sensitive hyperparameter.

## Connections

An early form of **conditional computation**, alongside [[Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer]]; the idea returns in Universal Transformers and early-exit models.
