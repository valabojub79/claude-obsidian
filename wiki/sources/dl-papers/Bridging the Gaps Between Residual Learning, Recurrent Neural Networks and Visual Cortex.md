---
type: source
title: "Bridging the Gaps Between Residual Learning, Recurrent Neural Networks and Visual Cortex"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1604.03640"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - cnn
  - rnn
  - neuroscience
status: ingested
address: c-000224
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Residual Networks]]"
  - "[[Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/bridging-gap-resnet-rnn.md]]"
---

# Bridging the Gaps Between Residual Learning, Recurrent Neural Networks and Visual Cortex

[Paper](https://arxiv.org/abs/1604.03640) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** The visual cortex isn't hundreds of layers deep, but it is recurrent. A ResNet with **weight sharing** across blocks is equivalent to an unrolled RNN with skip connections, and such shared-weight ResNets perform almost as well as unshared ones with far fewer parameters. The authors also generalize to multi-state recurrent systems mimicking cortical areas.

## Connections

Supports the view that depth can be traded for recurrence: [[Residual Networks]], [[Recurrent Neural Networks]].
