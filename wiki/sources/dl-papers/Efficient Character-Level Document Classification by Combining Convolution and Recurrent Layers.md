---
type: source
title: "Efficient Character-Level Document Classification by Combining Convolution and Recurrent Layers"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1602.00367"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - character-level
  - text-classification
status: ingested
address: c-000241
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Character-Level Convolutional Networks for Text Classification]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/efficient-char-level-document-classification-cnn-rnn.md]]"
---

# Efficient Character-Level Document Classification by Combining Convolution and Recurrent Layers

[Paper](http://arxiv.org/abs/1602.00367) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** **ConvRec**: a few conv layers over character embeddings, then an LSTM. It matches or beats deep char-CNNs with **10 to 50x fewer parameters**.

## Key points

- Word models treat related words as unrelated, can't handle OOV words, and have many parameters. Char-CNNs need many layers because receptive fields are small, and the RNN supplies long-range context instead.
- 8-d char embeddings; 2 to 5 conv layers (kernels 5 and 3, pool 2, ReLU); LSTM with 128 units; dropout. 96-character alphabet, Adadelta, batch 128, padding with masking, clipping at 5, early stopping.
- Beats large CNNs especially on **smaller datasets** (less overfitting). More filters or layers barely matter.

## Critique (Denny Britz)

Plot performance against parameter count; report training time.
