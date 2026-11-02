---
type: source
title: "Contextual LSTM (CLSTM) Models for Large Scale NLP Tasks"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1602.06291"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - language-modeling
  - rnn
status: ingested
address: c-000229
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/clstm-large-scale.md]]"
---

# Contextual LSTM (CLSTM) Models for Large Scale NLP Tasks

[Paper](http://arxiv.org/abs/1602.06291) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Append a **topic/context vector** to each LSTM input. Evaluated on language modeling, next-sentence selection and next-topic prediction on English Wikipedia (1.4B training words, 129k vocabulary). Beats LSTM baselines.

## Key points

- Topics come from an internal supervised classifier, computed over the current sentence prefix, the previous sentence, or the paragraph; using all of them is best.
- Given the current segment's topic, the previous sentence's topic adds nothing.
- Hidden state is not reset between sentences, yet explicit topic still helps.

## Critique (Denny Britz)

**More hidden units beat the topic features by a wide margin**, so the practical value is doubtful. The external topic classifier brings in data the baselines lacked. Why not unsupervised sentence embeddings (seq2seq autoencoders, PV) as context, or residual connections?
