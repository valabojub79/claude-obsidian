---
type: source
title: "Deep Networks with Stochastic Depth"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1603.09382"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - cnn
  - regularization
status: ingested
address: c-000231
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Residual Networks]]"
  - "[[Dropout]]"
  - "[[Deep Residual Learning for Image Recognition]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/stochastic-depth.md]]"
---

# Deep Networks with Stochastic Depth

[Paper](http://arxiv.org/abs/1603.09382) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Huang et al. **randomly drop entire residual blocks** during training, keeping only the identity shortcut. Survival probability decays linearly with depth (to 0.5 at the last block). This mitigates vanishing gradients and diminishing feature reuse, cuts training time, and set records on CIFAR-10, CIFAR-100 and SVHN.

## Key points

- Lower layers are kept more often (their features are more "fundamental").
- Training time is **25 to 50% lower**; gradient magnitudes measurably larger early in the network.
- At test time all blocks are active, with outputs scaled by survival probability, effectively an **ensemble of networks of different depths**.
- Enabled training **1000+ layer** ResNets with further error reductions.

## Connections

[[Dropout]] at the layer level; "drop path" is standard in modern vision Transformers.
