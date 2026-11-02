---
type: source
title: "A Sensitivity Analysis of (and Practitioners' Guide to) Convolutional Neural Networks for Sentence Classification"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1510.03820"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - cnn
  - hyperparameters
  - text-classification
status: ingested
address: c-000212
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Hyperparameter Tuning]]"
  - "[[Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/sensitivity-analysis-cnn-sentence-classification.md]]"
---

# A Sensitivity Analysis of (and Practitioners' Guide to) Convolutional Neural Networks for Sentence Classification

[Paper](http://arxiv.org/abs/1510.03820) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Zhang and Wallace run a large sweep (with variance estimates) over the hyperparameters of **Kim's (2014) one-layer CNN** across 7 sentence-classification datasets, and give practical recommendations.

## Recommended baseline

word2vec embeddings; filter region sizes **(3, 4, 5)**; **100** feature maps per size; **ReLU**; **1-max pooling**; dropout **0.5**; L2 norm constraint 3.

## Findings

- Pretrained embeddings beat one-hot; word2vec usually beats GloVe.
- Best region size is dataset-dependent (2 to 25). Line-search one size, then combine nearby sizes.
- More than about 600 feature maps per size rarely helps.
- ReLU and max-pooling are almost always best; dropout 0.1 to 0.5 helps; the norm constraint matters little.

## Critique (Denny Britz)

The datasets are all similar (short sentences, similar sizes); long documents or huge datasets might change the conclusions.
