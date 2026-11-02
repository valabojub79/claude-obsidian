---
type: source
title: "A Neural Attention Model for Abstractive Sentence Summarization"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1509.00685"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - summarization
  - attention
  - nlp
status: ingested
address: c-000208
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Beam Search]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/neural-attention-model-for-abstractive-sentence-summarization.md]]"
---

# A Neural Attention Model for Abstractive Sentence Summarization

[Paper](http://arxiv.org/abs/1509.00685) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Rush, Chopra and Weston's attention-based seq2seq model for **headline generation** (sentence-level abstractive summarization). Trained on (first sentence, headline) pairs from Gigaword.

## Key points

- Fixed-length outputs; beam-search decoding.
- **Extractive tuning**: a log-linear scoring layer with features encouraging words copied from the input.
- An early landmark of neural abstractive summarization, followed by copy and pointer-generator models.
