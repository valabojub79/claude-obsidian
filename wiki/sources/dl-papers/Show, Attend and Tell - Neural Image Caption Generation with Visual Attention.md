---
type: source
title: "Show, Attend and Tell - Neural Image Caption Generation with Visual Attention"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1502.03044"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - computer-vision
  - attention
  - captioning
status: ingested
address: c-000292
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Recurrent Models of Visual Attention]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/show-attend-tell.md]]"
---

# Show, Attend and Tell - Neural Image Caption Generation with Visual Attention

[Paper](http://arxiv.org/abs/1502.03044) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Xu et al. add **attention over CNN feature maps** (lower conv layer, before pooling, so locations survive) to an LSTM caption decoder. **Soft** attention is deterministic and trained by backprop; **hard** attention is stochastic and trained with sampling (REINFORCE-like). State of the art on Flickr8k, Flickr30k and MS COCO, plus **interpretable** attention maps showing where the model looks for each word.

## Key points

- Soft attention works as in seq2seq; which variant wins depends on the metric (BLEU vs METEOR).
- VGG features; MS COCO trains in about 3 days on a Titan Black.
- Maps are visualized by upsampling with Gaussian smoothing.

## Critique (Denny Britz)

When and why does soft beat hard? What is the compute overhead of attention?
