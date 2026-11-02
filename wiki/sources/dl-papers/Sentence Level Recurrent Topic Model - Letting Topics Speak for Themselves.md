---
type: source
title: "Sentence Level Recurrent Topic Model - Letting Topics Speak for Themselves"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1604.02038"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - topic-modeling
  - generative
status: ingested
address: c-000288
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Contextual LSTM (CLSTM) Models for Large Scale NLP Tasks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/slrtm.md]]"
---

# Sentence Level Recurrent Topic Model - Letting Topics Speak for Themselves

[Paper](https://arxiv.org/abs/1604.02038) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** An RNN topic model that respects **word order** and assumes all words in a sentence share a topic. Topic mixtures are drawn from a Dirichlet; a learned **topic embedding** conditions a generative LSTM. It clearly beats competing topic models in perplexity of generated sentences and on downstream classification, and generates sensible topic-conditioned sentences.
