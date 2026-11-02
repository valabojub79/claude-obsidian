---
type: source
title: "Deep Residual Learning for Image Recognition"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1512.03385"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - cnn
  - computer-vision
status: ingested
address: c-000234
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Residual Networks]]"
  - "[[Classic CNN Architectures]]"
  - "[[Training Very Deep Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/deep-residual-learning.md]]"
---

# Deep Residual Learning for Image Recognition

[Paper](http://arxiv.org/abs/1512.03385) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** He et al. introduce **ResNets**: shortcut connections let layers learn a residual `F(x) = H(x) - x`. 3.57% top-5 error on the ImageNet test set; **1st place in ILSVRC 2015**.

## Key points

- **Degradation problem:** deeper plain nets have higher *training* error. It's an optimization failure, not overfitting.
- In theory extra layers could learn the identity; in practice that's hard, while driving `F(x)` to 0 is easy.
- No extra parameters or FLOPs (identity shortcuts). Like [[Training Very Deep Networks|highway networks]], but with **always-open, data-independent** gates.
- Dimension change: zero-padding or a 1x1 projection (slightly better, "not worth" the parameters); **bottleneck** blocks with 1x1 convs for deep variants.
- Plain 18 vs 34 layers: 27.94 vs 28.54 top-1 error (deeper is worse). ResNet 18 vs 34: 27.88 vs **25.03**.
- A single ResNet beats previous ensembles.

## Critique (Denny Britz)

Lovely simplicity. How does skip length matter (only 2 to 3 layers were tested)? Recursive residuals? Why can't highway nets learn the same thing? Apply it to RNNs for long-range dependencies?

Concept page: [[Residual Networks]].
