---
type: source
title: "Neural Machine Translation with Reconstruction"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1611.01874"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
status: ingested
address: c-000268
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Dual Learning for Machine Translation]]"
  - "[[Beam Search]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nmt-with-reconstruction.md]]"
---

# Neural Machine Translation with Reconstruction

[Paper](https://arxiv.org/abs/1611.01874) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Tu et al. add a **reconstructor** RNN that regenerates the source from the decoder's hidden states (attending over them). The reconstruction likelihood is added to training and used to **rerank** beam candidates.

## Problem addressed

Seq2seq **under- and over-translates**: nothing ensures all source content is covered. MLE favors short outputs, so **bigger beams lower BLEU**.

## Results (Chinese-English, 1.25M pairs)

- Training only: BLEU 30.65 to 31.17 (beam 10).
- Plus reranking: **31.73**. BLEU now **rises with beam size**.

Setup: 30k vocabulary, max length 80, 620-d embeddings, 1000-d hidden, batch 80; 15 epochs of Adadelta, then 10 with the reconstructor.

## Critique (Denny Britz)

"Coverage" describes it better than "adequacy". Why does BLEU still drop with length normalization? Show loss curves, test on EN-FR and EN-DE, and consider iterative reconstruction. The authors responded in a GitHub issue on the repo.
