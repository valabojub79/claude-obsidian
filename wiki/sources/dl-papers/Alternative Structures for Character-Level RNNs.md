---
type: source
title: "Alternative Structures for Character-Level RNNs"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.06303"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - rnn
  - character-level
status: ingested
address: c-000218
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Language Models and Sequence Generation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/alternative-structure-char-rnn.md]]"
---

# Alternative Structures for Character-Level RNNs

[Paper](http://arxiv.org/abs/1511.06303) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Two ways to help character-level RNN language models: **mixed** (condition on a jointly trained word-level RNN, interpolating losses) and **cond** (condition the output softmax on preceding character n-grams, so the RNN needn't memorize them). Both beat plain char-RNNs in bits per character.

## Key points

- Char-RNNs need huge hidden states for long dependencies; word RNNs can't handle new vocabulary and need huge softmaxes.
- The n-gram conditioning works on arbitrary byte data (evaluated on binary data too).
- Constant learning rate, decayed when validation accuracy drops.

## Critique (Denny Britz)

Parameter counts aren't reported (the extra components cost parameters, so the comparison may be unfair); no LSTM or GRU experiments; bits per character is unintuitive; the "mixed" model is language-specific, which undercuts the "arbitrary data" argument; the n-gram model is under-explained.
