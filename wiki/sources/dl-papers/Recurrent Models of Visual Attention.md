---
type: source
title: "Recurrent Models of Visual Attention"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1406.6247"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - computer-vision
  - attention
  - reinforcement-learning
status: ingested
address: c-000282
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Show, Attend and Tell - Neural Image Caption Generation with Visual Attention]]"
  - "[[Spatial Transformer Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/recurrent-models-of-visual-attention.md]]"
---

# Recurrent Models of Visual Attention

[Paper](http://arxiv.org/abs/1406.6247) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Mnih et al.'s **Recurrent Attention Model (RAM)**: an RNN takes a low-resolution, multi-scale **glimpse**, then chooses where to look next and, eventually, what to predict. Computation depends on the number and size of glimpses, **not image size**. The model is non-differentiable (hard attention) and trained with **REINFORCE**. Evaluated on MNIST, cluttered MNIST and a dynamic game environment.

## Critique (Denny Britz)

"Independent of image size" is only partly true: bigger images need more or larger glimpses. MNIST-only benchmarks; training time not reported, so feasibility on large images is unclear.
