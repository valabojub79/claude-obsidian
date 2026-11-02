---
type: source
title: "A Unified Tagging Solution - Bidirectional LSTM Recurrent Neural Network with Word Embedding"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.00215"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - sequence-labeling
  - rnn
status: ingested
address: c-000214
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Recurrent Neural Networks]]"
  - "[[Word Embeddings]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/unified-tagging-blstm.md]]"
---

# A Unified Tagging Solution - Bidirectional LSTM Recurrent Neural Network with Word Embedding

[Paper](http://arxiv.org/abs/1511.00215) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Wang et al. use one **BiLSTM** with task-independent inputs (word plus capitalization) for **POS tagging, chunking and NER**, with a decoder restricted to valid tag sequences. They also propose a new embedding-pretraining task: **randomly replace words and predict which are wrong** (an ELECTRA-like idea, years early). On par with state of the art when using pretrained embeddings.

## Key points

100-d embeddings and cells, 1 or 2 layers; bigger cells barely help.

## Critique (Denny Britz)

The task-specific decoder undercuts the "task-independent" claim (probably needed only because data is small). Comparisons are unfair given 600M+ words of external embedding pretraining. Why not one multi-task model?
