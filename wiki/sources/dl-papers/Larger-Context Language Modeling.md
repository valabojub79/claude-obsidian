---
type: source
title: "Larger-Context Language Modeling"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.03729"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - language-modeling
status: ingested
address: c-000253
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Contextual LSTM (CLSTM) Models for Large Scale NLP Tasks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/larger-context-lm.md]]"
---

# Larger-Context Language Modeling

[Paper](http://arxiv.org/abs/1511.03729) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Wang and Cho condition an LSTM language model on **previous sentences**.

- **Context representation:** bag of words over N sentences; sequential BoW (one per sentence, through an LSTM); or sequential BoW with **attention**.
- **Fusion:** early (context as LSTM input) or **late** (an extra LSTM gate for context, which helps against vanishing gradients).

Perplexity improves on IMDB, BBC and PTB; sequential BoW with attention and late fusion does best. **Noun phrases** benefit most.

## Key points

- Sequential BoW **without** attention performs poorly.
- 1000-unit LSTMs, Adadelta, sentences up to 50 words.

## Critique (Denny Britz)

Important: treating sentences independently makes LMs corpus-specific. Why not skip-thought or paragraph vectors as context? The "fixed-vector bottleneck" explanation is unconvincing for such short sequences. Visualize attention. Relying on sentence boundaries is a limitation.
