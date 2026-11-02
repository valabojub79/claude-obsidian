---
type: source
title: "Learning to Execute"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1410.4615"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - program-synthesis
  - curriculum-learning
status: ingested
address: c-000259
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
  - "[[Neural Turing Machines]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/learning-to-execute.md]]"
---

# Learning to Execute

[Paper](http://arxiv.org/abs/1410.4615) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Zaremba and Sutskever show seq2seq LSTMs (2 layers of 400 cells, about 2.5M parameters) can **evaluate short Python programs** (loops, conditionals, add, subtract, multiply) read character by character, outputting the result from a 12-symbol vocabulary. A new **curriculum** strategy is key.

## Curriculum strategies

1. **Naive**: increase difficulty over time.
2. **Mixed**: random mix of easy and hard.
3. **Combined**: naive plus mixed. Mixed or combined almost always wins; naive can hurt because the LSTM must restructure its memory.

## Key points

- Tricks: **reverse** and **double** the input, both of which help a lot.
- Evaluated with teacher forcing. Tasks: program evaluation, addition, memorization.
- Nested loops are hard; LSTMs lack compositionality.

## Critique (Denny Britz)

Is mixing difficulties related to regularization such as dropout, since both force general representations?
