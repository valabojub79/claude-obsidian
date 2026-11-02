---
type: source
title: "Neural Machine Translation with Recurrent Attention Modeling"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1607.05108"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - attention
status: ingested
address: c-000269
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Recurrent Neural Machine Translation]]"
  - "[[Attention Mechanism]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nmt-rec-attention.md]]"
---

# Neural Machine Translation with Recurrent Attention Modeling

[Paper](https://arxiv.org/abs/1607.05108) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Standard attention ignores **where it attended before**, though that history predicts the next focus. Add a dynamic memory that tracks attention over time (a window of `k` steps) for each source word. Beats competing models on English-German and English-Chinese.

## Critique (Denny Britz)

How costly and how hard to train? Attending sequentially to neighbors suits some language pairs, not others; the fixed `k` window is restrictive.
