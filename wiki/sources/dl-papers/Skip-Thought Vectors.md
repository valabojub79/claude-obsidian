---
type: source
title: "Skip-Thought Vectors"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.06726"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - embeddings
  - unsupervised
status: ingested
address: c-000293
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Word2Vec and Negative Sampling]]"
  - "[[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/skip-thought-vectors.md]]"
---

# Skip-Thought Vectors

[Paper](http://arxiv.org/abs/1506.06726) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Kiros et al. lift **skip-gram to sentences**. An encoder GRU encodes a sentence; two decoders reconstruct the **previous and next sentences**. The resulting generic **skip-thought vectors**, used as features with linear models, are competitive on semantic relatedness, paraphrase and classification, though below task-specific fine-tuned models.

## Key points

- BookCorpus (74M sentences, 1B tokens); about 2 weeks of training.
- uni-skip (2400-d) and bi-skip (1200-d per direction), often concatenated; GRUs, Adam, clipping at 10.
- **Vocabulary expansion**: learn a linear map from word2vec space into the encoder's embedding space to handle unseen words.

## Critique (Denny Britz)

How would non-linear classifiers do on top? Poor story generation suggests weak long-range modeling; deeper encoders or attention might help.
