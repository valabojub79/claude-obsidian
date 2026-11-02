---
type: source
title: "ReNet - A Recurrent Neural Network Based Alternative to Convolutional Networks"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1505.00393"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - computer-vision
  - rnn
status: ingested
address: c-000280
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Convolutional Neural Networks]]"
  - "[[Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/renet-rnn-alternative-to-convnet.md]]"
---

# ReNet - A Recurrent Neural Network Based Alternative to Convolutional Networks

[Paper](http://arxiv.org/abs/1505.00393) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Visin et al. (LISA) replace conv and pool layers with **four RNNs per layer** sweeping over image patches vertically (both directions) and then horizontally (both directions). Each output therefore sees **whole-image context**, unlike local convolutions. A viable alternative, though it doesn't beat CNNs.

## Key points

2 ReNet layers of 256-d on 2x2 patches, 4096-d fully connected layers; flip and shift augmentation.

## Critique (Denny Britz)

Training time and complexity versus a CNN? Why patches at all, and why so small? Try full-height patches.
