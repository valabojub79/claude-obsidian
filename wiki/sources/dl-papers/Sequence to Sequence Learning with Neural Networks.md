---
type: source
title: "Sequence to Sequence Learning with Neural Networks"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1409.3215"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - sequence-models
  - rnn
status: ingested
address: c-000290
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence to Sequence Models]]"
  - "[[Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/seq2seq-with-neural-networks.md]]"
---

# Sequence to Sequence Learning with Neural Networks

[Paper](http://arxiv.org/abs/1409.3215) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Sutskever, Vinyals and Le's seq2seq paper: a deep **4-layer LSTM encoder-decoder** (1000 cells per layer, 1000-d embeddings, 160k source and 80k target vocabularies) reaches **34.8 BLEU** on WMT'14 EN-FR on its own, and near state of the art when reranking SMT output. Surprisingly, it **handles long sentences** well.

## Key points

- **Reversing the source** helps a lot, probably by creating short-range dependencies between corresponding words. The authors have "no complete explanation".
- **Deep beats shallow**; separate encoder and decoder parameters.
- 12M sentences (652M words); SGD lr 0.7, halved every epoch after 5; gradient clipping; 6.3k words/s on GPUs. Length bucketing gives 2x speed.
- PCA of sentence vectors gives meaningful clusters, invariant to active vs passive voice.
- Beam size 1 already good; 2 is best.

## Critique (Denny Britz)

Much of the success is compute and engineering; attention might do better with equal resources. Reversing the input is a hack; a principled fix for long-range dependencies is needed (attention provided it).

Concept page: [[Sequence to Sequence Models]].
