---
type: source
title: "On the Properties of Neural Machine Translation - Encoder-Decoder Approaches"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1409.1259"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - analysis
status: ingested
address: c-000274
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation by Jointly Learning to Align and Translate]]"
  - "[[Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/properties-of-neural-mt.md]]"
---

# On the Properties of Neural Machine Translation - Encoder-Decoder Approaches

[Paper](http://arxiv.org/abs/1409.1259) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Cho et al. analyze early encoder-decoder NMT. Quality **degrades sharply with sentence length and with the number of unknown words**, so long-range dependencies and large vocabularies need work. They also introduce the **gated recursive convolutional network (grConv)**, a binary-tree encoder with gated (left, right, reset) composition. It underperforms the RNN encoder but appears to learn grammatical structure without supervision.

## Key points

- Decoder always an RNN; encoder an RNN or grConv. 30k vocabulary, trained only on sentences of 30 tokens or fewer, not to convergence; length-normalized beam search.
- Hypothesis: the fixed vector is a bottleneck (confirmed by attention, in [[Neural Machine Translation by Jointly Learning to Align and Translate]]).

## Critique (Denny Britz)

Training only on short sentences can't be expected to generalize to long ones. Typo: the time superscript in the activation formula should be `t-1`.
