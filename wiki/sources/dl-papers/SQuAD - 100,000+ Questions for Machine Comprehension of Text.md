---
type: source
title: "SQuAD - 100,000+ Questions for Machine Comprehension of Text"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1606.05250"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - reading-comprehension
  - dataset
status: ingested
address: c-000286
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Teaching Machines to Read and Comprehend]]"
  - "[[Pointer Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/squad.md]]"
---

# SQuAD - 100,000+ Questions for Machine Comprehension of Text

[Paper](http://arxiv.org/abs/1606.05250) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Rajpurkar et al. (Stanford) release the **Stanford Question Answering Dataset**: about 100k crowdsourced questions on about 500 Wikipedia articles, where the answer is a **span** of the passage.

## Key points

- Answer types: 20% dates and numbers, 32% proper nouns, 31% noun phrases, 16% other phrases.
- `O(N^2)` candidate spans per passage.
- **Humans: 77% exact match, 86% F1** (ambiguous span boundaries cap EM). A feature-rich **logistic regression baseline: 51% F1**. Lexicalized and dependency-path features matter most; it does best on dates, numbers and single tokens.

## Connections

The benchmark that drove 2016-2018 reading comprehension (BiDAF and others) until BERT passed human F1. Span pointing relates to [[Pointer Networks]].
