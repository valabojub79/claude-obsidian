---
type: source
title: "Target-Dependent Sentiment Classification with Long Short Term Memory"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1512.01100"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - sentiment
  - rnn
status: ingested
address: c-000297
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
  - "[[GloVe]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/target-dependent-sentiment-lstm.md]]"
---

# Target-Dependent Sentiment Classification with Long Short Term Memory

[Paper](http://arxiv.org/abs/1512.01100) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Tang et al. classify sentiment **toward a specific target** in a sentence:

- **TD-LSTM**: two LSTMs run toward the target, one from the left and one from the right; concatenate their final states and predict.
- **TC-LSTM**: also feed the averaged target-phrase vector at every step.

State of the art on a Twitter target-sentiment dataset.

## Key points

Pretrained embeddings make a huge difference: the best results need 200-d **GloVe**.

## Critique (Denny Britz)

Most of the gain comes from the embeddings; without them the models underperform simpler ones. Would the baselines with the same embeddings do as well? Attention was tried but failed (the corpus is small).
