---
type: source
title: "Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1406.1078"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - rnn
  - sequence-models
status: ingested
address: c-000258
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Gated Recurrent Unit]]"
  - "[[Sequence to Sequence Models]]"
  - "[[Sequence to Sequence Learning with Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/learning-phrase-representations.md]]"
---

# Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation

[Paper](http://arxiv.org/abs/1406.1078) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Cho et al. introduce the **RNN encoder-decoder** (encode to a fixed vector, decode a variable-length output) **and the GRU** cell. Used as an extra feature (phrase-pair scores) in a phrase-based SMT log-linear model, it improves BLEU, and it learns syntactically and semantically meaningful phrase representations.

## Key points

- Usable for scoring or generation; could replace the whole pipeline but doesn't yet.
- 15k vocabulary (93% coverage), 100-d embeddings, 500 maxout units, batch 64, Adagrad, 384M words, 3 days of training.
- Trained without phrase-frequency information, so it captures linguistic rather than statistical regularities.

## Critique (Denny Britz)

Why invent a new unit instead of using LSTM? (In hindsight GRU became a standard: [[Gated Recurrent Unit]].)
