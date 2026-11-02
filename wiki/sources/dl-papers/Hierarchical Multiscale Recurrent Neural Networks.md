---
type: source
title: "Hierarchical Multiscale Recurrent Neural Networks"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1609.01704"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - language-modeling
status: ingested
address: c-000250
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
  - "[[Adaptive Computation Time for Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/hm-rnn.md]]"
---

# Hierarchical Multiscale Recurrent Neural Networks

[Paper](https://arxiv.org/abs/1609.01704) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Chung, Ahn and Bengio's HM-RNN learns hierarchical **and** temporal structure (characters, words, phrases) **without being told the boundaries**. Each layer has a binary **boundary detector** that chooses one of three operations:

| Op | When | What |
|----|------|------|
| UPDATE | own segment ongoing, layer below finished | standard LSTM update |
| COPY | neither finished | copy previous cell (wait) |
| FLUSH | own segment finished | pass summary upward, reset |

Binary decisions are trained with a **straight-through estimator** (hard sigmoid) plus **slope annealing**.

## Claimed benefits

Computation saved (higher layers update rarely), better long-range gradient flow, and resource allocation per level.

## Results

Slightly beats state of the art on PTB; matches or beats it on Text8 and Hutter Prize; handwriting generation beats a standard LSTM. It discovers spaces and word boundaries.

## Critique (Denny Britz)

Important ideas, disappointing margins. Far more complex than, say, a batch-normalized LSTM; it wins narrowly with tricks (a suspicious slope-annealing constant of 0.04). Handwriting is only compared to a plain LSTM. Depth still fixes the number of hierarchy levels. Boundary discovery may not be novel (LSTMs likely learn it too). Efficiency is claimed but not measured. Try it on CJK languages.
