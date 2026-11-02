---
type: source
title: "Effective Approaches to Attention-Based Neural Machine Translation"
source_type: paper
year: 2015
url: "https://arxiv.org/abs/1508.04025"
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
address: c-000240
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Neural Machine Translation by Jointly Learning to Align and Translate]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/effective-approaches-nmt-attention.md]]"
---

# Effective Approaches to Attention-Based Neural Machine Translation

[Paper](https://arxiv.org/abs/1508.04025) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Luong, Pham and Manning compare **global** attention (over all source words) and **local** attention (a window around a predicted position). State of the art on WMT'14 and '15 English-German.

## Key points

- Attentional hidden state `h~_t = tanh(W_c [c_t; h_t])` feeds the softmax.
- Score functions: **dot** `h_t . h_s`; **general** `h_t^T W_a h_s`; **concat** `v^T tanh(W_a [h_t; h_s])` (Bahdanau-style). For global attention the **simple dot score works best**.
- Local attention: predict aligned position `p_t` and attend within `[p_t - D, p_t + D]`.
- Setup: 50k vocabulary, 4-layer LSTM, 1000-d, unidirectional encoder, gradient clipping at 5, dropout 0.2, SGD with decay. UNK replacement adds 1.9 BLEU.

## Connections

"Luong attention" (multiplicative) vs "Bahdanau attention" (additive). Dot-product scoring led to Transformer attention. See [[Attention Mechanism]].
