---
type: source
title: "A Neural Network Approach to Context-Sensitive Generation of Conversational Responses"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1506.06714"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
status: ingested
address: c-000210
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[A Neural Conversational Model]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nn-context-sentitive-responses.md]]"
---

# A Neural Network Approach to Context-Sensitive Generation of Conversational Responses

[Paper](http://arxiv.org/abs/1506.06714) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Sordoni et al. generate response `r` from (context `c`, message `m`) on **29M Twitter triples**:

- **RLMT**: a recurrent LM over the concatenated `(c, m, r)`.
- **DCGM-I**: `c` and `m` as one bag of words, through a feed-forward encoder, then an RNN decoder.
- **DCGM-II**: same, but `c` and `m` kept separate.

50k vocabulary, NCE loss. Quality degrades after about 8 generated tokens.

## Critique (Denny Britz)

A one-message "context" defeats the purpose, since real conversations are longer. Why complain about long sequences and not use LSTM or GRU?
