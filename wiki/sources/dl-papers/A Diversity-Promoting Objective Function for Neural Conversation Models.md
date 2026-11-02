---
type: source
title: "A Diversity-Promoting Objective Function for Neural Conversation Models"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1510.03055"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - dialogue
  - decoding
status: ingested
address: c-000207
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[A Neural Conversational Model]]"
  - "[[Diverse Beam Search - Decoding Diverse Solutions from Neural Sequence Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/diversity-promoting-objective-ncm.md]]"
---

# A Diversity-Promoting Objective Function for Neural Conversation Models

[Paper](http://arxiv.org/abs/1510.03055) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Li et al. train with maximum likelihood but **decode with Maximum Mutual Information (MMI)** to avoid generic replies like "I don't know". Two forms: **MMI-antiLM** (subtract a language-model score) and **MMI-bidi** (rerank by `p(source | response)`).

## Key points

- Generic, high-frequency replies are partly caused by the likelihood objective.
- 4-layer LSTM, 1000-d states and embeddings. Data: Twitter (129M context-message-response triples) and OpenSubtitles (70M noisy lines without speaker turns).
- Perplexity is the wrong metric when you deliberately avoid high-probability replies; evaluated with BLEU, humans and qualitative analysis.

## Critique (Denny Britz)

Shouldn't more diversity *lower* BLEU? And "artificially" promoting diversity feels wrong: it should emerge from context and intention.
