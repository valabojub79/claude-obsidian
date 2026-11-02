---
type: source
title: "Using Fast Weights to Attend to the Recent Past"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.06258"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - memory
  - attention
status: ingested
address: c-000302
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Layer Normalization]]"
  - "[[Adaptive Computation Time for Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/fast-weight-to-attend.md]]"
---

# Using Fast Weights to Attend to the Recent Past

[Paper](https://arxiv.org/abs/1610.06258) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Ba, Hinton et al. add **fast weights**, a quickly decaying associative memory between slow weights (long-term) and hidden state (short-term):

```
A(t+1) = lambda * A(t) + eta * h(t) h(t)^T
```

An inner loop applies `A` to refine the next hidden state. That is equivalent to attending over recent hidden states in proportion to their similarity with the current one, but cheap. Uses [[Layer Normalization]] for stability.

## Results

- Associative retrieval (recall recent key-value pairs): far better than RNN, LSTM and Associative LSTM.
- Glimpse-based MNIST: beats RNN and LSTM, comparable to a ConvNet.
- RL agents in partially observable environments learn faster.

## Critique (Denny Britz)

Exciting, and reminiscent of ACT's "pondering", but experiments use **S = 1** inner step, the point of extra computation is untested, and there are no NLP experiments.

## Connections

Fast weights are formally linked to **linear attention**, now a revived research line ("linear Transformers are fast weight programmers").
