---
type: source
title: "Layer Normalization"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1607.06450"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - normalization
  - rnn
status: ingested
address: c-000255
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Batch Normalization]]"
  - "[[Batch Normalization - Accelerating Deep Network Training]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/layer-norm.md]]"
---

# Layer Normalization

[Paper](https://arxiv.org/abs/1607.06450) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Ba, Kiros and Hinton normalize across the **units of a layer for a single example**, instead of across the batch. It needs no batch statistics, so it suits **RNNs**, variable-length sequences and small batches, and train and test behavior are identical.

```
mu = mean_i(a_i);  sigma = std_i(a_i);  h = g * (a - mu) / sigma + b
```

## Findings

Faster convergence, sometimes better optima, versus batch-normalized or unnormalized RNNs. For **CNNs, BatchNorm still wins**.

## Connections

LayerNorm became the standard normalization in Transformers (pre-LN, and the RMSNorm variant). Compare [[Batch Normalization]].
