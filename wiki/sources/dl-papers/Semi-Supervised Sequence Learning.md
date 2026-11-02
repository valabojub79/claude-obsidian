---
type: source
title: "Semi-Supervised Sequence Learning"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.01432"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - pretraining
  - transfer-learning
status: ingested
address: c-000287
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Unsupervised Pretraining]]"
  - "[[Transfer Learning]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/semi-supervised-sequence-learning.md]]"
---

# Semi-Supervised Sequence Learning

[Paper](http://arxiv.org/abs/1511.01432) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Dai and Le **pretrain an LSTM on unlabeled text**, either as a **sequence autoencoder** (SA-LSTM: reconstruct the input from the final state) or as a **language model** (LM-LSTM), then **fine-tune** on classification. More stable training, better generalization, and state of the art on several benchmarks. Unlabeled data compensates for scarce labels.

## Results (error; previous best in parentheses)

IMDB **7.24%** (7.42%) · Rotten Tomatoes 16.7% (18.5%, with extra unlabeled data) · 20 Newsgroups 15.6% (17.1%) · DBpedia character-level 1.19% (1.74%).

## Key points

LSTM with 1024 cells, 512-d embeddings, 512-d hidden layer with 50% dropout; truncated BPTT over 400 steps; clipped cell outputs and gradients; word and embedding dropout tuned on dev. "Linear gain": inject targets at every step with linearly increasing weights.

## Critique (Denny Britz)

When does linear gain help or hurt? Word dropout is unexplained. Joint training is evaluated only on IMDB. Only classification tasks; what about seq2seq? Training time and batching aren't given.

## Connections

The direct precursor of ULMFiT, ELMo, GPT and BERT: **pretrain an LM, then fine-tune**. See [[Unsupervised Pretraining]].
