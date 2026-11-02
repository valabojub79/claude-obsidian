---
type: source
title: "Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1507.04808"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - rnn
status: ingested
address: c-000225
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[A Neural Conversational Model]]"
  - "[[Sequence to Sequence Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/e2e-dialog-ghnnm.md]]"
---

# Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models

[Paper](http://arxiv.org/abs/1507.04808) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Serban et al. apply **HRED** (Hierarchical Recurrent Encoder-Decoder) to dialogue. An utterance encoder turns words into a thought vector; a context encoder runs over utterance vectors; a decoder generates the reply. On **MovieTriples** it beats plain RNNs and DCGM in perplexity; **pretraining** on a 5M Q-A pair corpus helps much more.

## Key points

- GRUs, about 300-d states, 10k vocabulary; entities and numbers removed with NLTK. Context is only one previous utterance.
- About 200k training triples. Pretraining cuts perplexity by about 10 points; architecture choices change it by about 1.
- Most good predictions are **generic**, so BLEU favors pronouns and punctuation and is a poor metric.

## Critique (Denny Britz)

Would a larger dataset remove the need for pretraining? What about longer contexts?
