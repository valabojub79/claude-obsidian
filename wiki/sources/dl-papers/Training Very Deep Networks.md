---
type: source
title: "Training Very Deep Networks"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1507.06228"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - cnn
  - optimization
status: ingested
address: c-000301
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Residual Networks]]"
  - "[[Deep Residual Learning for Image Recognition]]"
  - "[[Character-Aware Neural Language Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/training-very-deep-networks.md]]"
---

# Training Very Deep Networks

[Paper](http://arxiv.org/abs/1507.06228) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Srivastava, Greff and Schmidhuber's **Highway Networks**: LSTM-style gates on feed-forward layers:

```
y = H(x) * T(x) + x * (1 - T(x))      # transform gate T, carry gate C = 1 - T
```

Networks with **tens to hundreds of layers** train with plain SGD. Competitive on MNIST, CIFAR-10 and CIFAR-100 with fewer parameters.

## Key points

- Gates force equal input and output sizes; use plain layers to change dimensions.
- **Initialize transform-gate biases negative** (-1 to -3), so layers start by carrying their input through.
- Routing is **input-dependent**, not fixed. Lesioning shows each layer matters on complex data.

## Critique (Denny Britz)

No dropout experiments; does gating reduce dropout's value? If some gates barely vary across inputs, could you prune to a fixed, faster structure?

## Connections

[[Residual Networks]] are the gate-free, always-open special case, which turned out easier to optimize. Highway layers are key in [[Character-Aware Neural Language Models]].
