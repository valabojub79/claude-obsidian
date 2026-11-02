---
type: source
title: "Recurrent Memory Network for Language Modeling"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1601.01272"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - language-modeling
  - attention
  - memory
status: ingested
address: c-000281
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[End-To-End Memory Networks]]"
  - "[[Alternative Structures for Character-Level RNNs]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/rmn-language-modeling.md]]"
---

# Recurrent Memory Network for Language Modeling

[Paper](http://arxiv.org/abs/1601.01272) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Tran, Bisazza and Monz add a **Memory Block** (attention over the last `n` input words, keyed by the current hidden state) on top of an LSTM. **RM** (LSTM + MB) and **RMR** (LSTM + MB + LSTM) come in 8 variants: optional temporal bias matrix, gated vs linear output. State-of-the-art LM perplexity on English, German and Italian.

## Key points

- RM with gating usually beats RMR.
- 128-d everything, memory size 15; SGD for 15 epochs, halving after epoch 4.
- Attention analysis: mostly recent words, but it also captures long-distance dependencies (German separable verbs) and discovers dependency types.

## Critique (Denny Britz)

Compare with feeding n-grams to the classifier ([[Alternative Structures for Character-Level RNNs]]). No related-work section; "memory" is a stretch, since it's one hop, i.e. plain attention. Why is RMR worse? Is 128-d too small?
