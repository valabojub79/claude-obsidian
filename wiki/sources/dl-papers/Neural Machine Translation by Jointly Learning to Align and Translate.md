---
type: source
title: "Neural Machine Translation by Jointly Learning to Align and Translate"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1409.0473"
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
address: c-000265
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Sequence to Sequence Models]]"
  - "[[Effective Approaches to Attention-Based Neural Machine Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nmt-jointly-learning-to-align-and-translate.md]]"
---

# Neural Machine Translation by Jointly Learning to Align and Translate

[Paper](http://arxiv.org/abs/1409.0473) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Bahdanau, Cho and Bengio introduce **attention**. Rather than compressing the source into one vector, the decoder computes, at each step, a softmax-weighted average of encoder states. The weights come from a small learned alignment network. New state of the art for NMT, with big gains on **long sentences**.

## Setup and results

Bidirectional GRU encoder with 1000 units (forward and backward states concatenated), maxout output layer. WMT'14 EN-FR BLEU **36.15** (on sentences without unknown words).

## Key points

- Cost is a `len(x) * len(y)` attention matrix.
- Gains are largest for long sentences, confirming the fixed-vector **bottleneck**.
- Attention matrices for EN-FR are near-diagonal, a soft word alignment learned without supervision.

## Critique (Denny Britz)

The weighted average is simple. What about attention functions where input states interact? (Self-attention later did exactly that.)

Concept page: [[Attention Mechanism]].
