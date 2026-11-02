---
type: source
title: "Character-Level Convolutional Networks for Text Classification"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1509.01626"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - cnn
  - character-level
  - text-classification
status: ingested
address: c-000228
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Convolutional Neural Networks]]"
  - "[[Text Understanding from Scratch]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/character-level-cnn-for-text-classification.md]]"
---

# Character-Level Convolutional Networks for Text Classification

[Paper](http://arxiv.org/abs/1509.01626) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Zhang, Zhao and LeCun use a 9-layer CNN (6 conv/pool plus 3 fully connected layers) on **one-hot characters**, with fixed input length 1014. It's competitive across large text-classification datasets they built.

## Key points

- Optional thesaurus-based data augmentation.
- **n-gram TF-IDF baselines win on small datasets** (up to 500k examples); the CNN wins above about 1M.

## Critique (Denny Britz)

A fixed 1014-character cutoff versus full-document word models is unfair, and there are no dataset length statistics. "No word knowledge" sits oddly with an English thesaurus. Very deep means very data-hungry: were shallower nets tried? Would unsupervised pretraining reduce the data needs?
