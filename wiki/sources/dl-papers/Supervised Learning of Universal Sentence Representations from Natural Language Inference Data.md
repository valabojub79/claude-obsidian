---
type: source
title: "Supervised Learning of Universal Sentence Representations from Natural Language Inference Data"
source_type: paper
year: 2017
url: "https://arxiv.org/abs/1705.02364"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - embeddings
  - transfer-learning
status: ingested
address: c-000296
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Skip-Thought Vectors]]"
  - "[[A Structured Self-Attentive Sentence Embedding]]"
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/supervised-learning-of-universal-sentence-representations.md]]"
---

# Supervised Learning of Universal Sentence Representations from Natural Language Inference Data

[Paper](https://arxiv.org/abs/1705.02364) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Conneau et al.'s **InferSent**: train sentence encoders **supervised on SNLI** (entailment, contradiction, neutral) and transfer them. They beat unsupervised encoders such as skip-thought on 12 transfer tasks: sentiment, subjectivity, SICK entailment and relatedness, caption-image retrieval and more.

## Encoders compared

LSTM or GRU (last state); **BiLSTM with mean or max pooling**; self-attentive BiLSTM; hierarchical ConvNet (an AdaSent variant, max-pooling every layer, concatenated).

**Winner: BiLSTM with max-pooling, 4096-d.** NLI forces semantic representations. Some encoders **over-specialize**: better on SNLI, worse at transfer. PyTorch code at facebookresearch/InferSent. (Note contributed to the repo by a community member.)
