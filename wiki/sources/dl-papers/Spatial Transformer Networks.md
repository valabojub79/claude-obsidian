---
type: source
title: "Spatial Transformer Networks"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.02025"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - computer-vision
  - attention
status: ingested
address: c-000294
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Convolutional Neural Networks]]"
  - "[[Recurrent Models of Visual Attention]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/spatial-transformer-networks.md]]"
---

# Spatial Transformer Networks

[Paper](http://arxiv.org/abs/1506.02025) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Jaderberg et al. (DeepMind) build a differentiable **Spatial Transformer** module that can be inserted anywhere in a network. It has three parts:

1. A **localization net** predicts transformation parameters `theta` from the input.
2. A **grid generator** maps output coordinates to input sampling points.
3. A (bilinear) **sampler** produces the warped output.

It learns input-dependent cropping, translation, rotation, scaling, skew and attention, end to end with backprop. State of the art on distorted MNIST, Street View House Numbers and CUB-200 birds (fine-grained).

## Key points

- Dynamic per example; fast, with little training overhead; `theta` can feed higher layers.
- Attention is a special case (crop plus scale) that also saves computation.
- Use in RNNs left for future work.

## Connections

Gives CNNs learned invariance beyond pooling; differentiable alternative to [[Recurrent Models of Visual Attention|hard-attention glimpses]].
