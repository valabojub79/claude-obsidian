---
type: source
title: "Recurrent Neural Network Regularization"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1409.2329"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - regularization
status: ingested
address: c-000284
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Dropout]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/rnn-regularization.md]]"
---

# Recurrent Neural Network Regularization

[Paper](http://arxiv.org/abs/1409.2329) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Zaremba, Sutskever and Vinyals show that [[Dropout]] works for LSTMs if applied **only to non-recurrent connections** (between layers at the same time step), never on the recurrent path. That keeps memory intact while regularizing.

## Results

| Task | Score |
|------|-------|
| PTB language modeling | perplexity **78.4** |
| Icelandic speech (Google) | 70.5% frame accuracy |
| WMT'14 EN to FR | BLEU 29.03 |
| MS COCO captioning | BLEU 24.3 |

## Connections

The standard "Zaremba dropout" recipe; later refined by variational (same-mask-per-sequence) dropout and AWD-LSTM.
