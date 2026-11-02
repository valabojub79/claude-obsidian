---
type: source
title: "Text Understanding from Scratch"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1502.01710"
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
address: c-000299
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Character-Level Convolutional Networks for Text Classification]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/text-understanding-from-scratch.md]]"
---

# Text Understanding from Scratch

[Paper](http://arxiv.org/abs/1502.01710) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Zhang and LeCun apply 6 and 9-layer (plus 3 fully connected) **ConvNets to one-hot characters**, with no word embeddings or word notion, on new large classification datasets. They beat bag-of-words and word2vec baselines. (The precursor of [[Character-Level Convolutional Networks for Text Classification]].)

## Datasets (train size) and accuracy (small / large model)

DBpedia 560k: 98.02 / 98.27 · Amazon 5-class 3M: 59.47 / 58.69 · Amazon polarity 3.6M: 94.50 / 94.49 · Yahoo Answers 1.4M: 70.16 / 70.45 · AG News 120k: 84.35 / 87.18 · Sogou (romanized Chinese) 450k: 91.35 / 95.12.

Filters of size 7 and 3; about 5 days per epoch on large Amazon; thesaurus-based synonym augmentation gives small gains.

## Critique (Denny Britz)

"Understanding" is claimed, but only classification is tested; no evidence it learns more than n-grams. No data-size ablation; weak baselines (no Kim CNN). Romanizing Chinese and using a word thesaurus contradict the "language-independent, from scratch" claim. No dev set or tuning details. Datasets weren't released (yet they complain about the lack of open data). Interesting: the Amazon confusion matrix doesn't show negation errors, which hints at meaningful representations.
