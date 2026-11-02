---
type: source
title: "Multi-task Sequence to Sequence Learning"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.06114"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - multi-task
  - sequence-models
  - nmt
status: ingested
address: c-000262
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Multi-Task Learning]]"
  - "[[Skip-Thought Vectors]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/multitask-seq2seq.md]]"
---

# Multi-task Sequence to Sequence Learning

[Paper](http://arxiv.org/abs/1511.06114) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Luong et al. show that jointly training seq2seq tasks improves a **reference task**. Three settings:

- **One-to-many**: EN to DE translation plus EN parsing. Both improve; even a small share of parsing updates helps translation noticeably.
- **Many-to-one**: image captioning plus DE to EN translation. Both improve.
- **Many-to-many**: translation plus unsupervised objectives. **Skip-thought helps; sequence autoencoders hurt.**

## Key points

4-layer LSTM with 1000 units, batch 128, dropout 0.2, SGD lr 0.7 with decay; **no attention**. A per-task **mixing ratio** relative to the reference task is a new hyperparameter.

## Critique (Denny Britz)

Promising for general multi-task systems (classification could slot in too). But how were mixing ratios chosen, and how sensitive are results to them? Cherry-picking is possible. Why would autoencoders actively hurt?
