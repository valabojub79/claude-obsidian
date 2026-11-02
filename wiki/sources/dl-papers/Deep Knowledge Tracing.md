---
type: source
title: "Deep Knowledge Tracing"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.05908"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - education
status: ingested
address: c-000230
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/deep-knowledge-tracing.md]]"
---

# Deep Knowledge Tracing

[Paper](http://arxiv.org/abs/1506.05908) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Piech et al. model a student's evolving knowledge with an RNN or LSTM. Input: the exercise attempted plus correctness (one-hot or embedded). Output: the probability of answering each future exercise correctly. It significantly beats Bayesian Knowledge Tracing and enables curriculum optimization and discovery of exercise relationships.

## Key points

- 200-d hidden layer, output dropout, NLL loss.
- **No expert concept annotation** needed.
- Curriculum experiment: **blocking** (runs of same-type exercises) beat mixing.

## Critique (Denny Britz)

Could it predict the student's likely *wrong answer*, revealing misconceptions?
