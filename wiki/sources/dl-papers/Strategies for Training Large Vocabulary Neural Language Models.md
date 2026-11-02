---
type: source
title: "Strategies for Training Large Vocabulary Neural Language Models"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1512.04906"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - language-modeling
  - softmax-approximation
status: ingested
address: c-000295
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Word2Vec and Negative Sampling]]"
  - "[[Exploring the Limits of Language Modeling]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/strategies-for-training-large-vocab-lm.md]]"
---

# Strategies for Training Large Vocabulary Neural Language Models

[Paper](http://arxiv.org/abs/1512.04906) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Chen, Grangier and Auli compare **softmax, hierarchical softmax, differentiated softmax (new), target sampling, NCE and self-normalization**, under a fixed **one-week** training budget, on PTB (10k vocabulary, 1M tokens), Gigaword (100k, 5B) and Billion Word (800k, 800M).

## Findings

- What works for small vocabularies isn't what works for large ones. Full softmax is fine at 10k and 100k but loses at 800k (too slow per example).
- **Differentiated softmax**: give frequent words larger output embeddings and rare words smaller ones (separate matrices per frequency band). Strong at large vocabulary sizes.
- Perplexity gains flatten after about 500M tokens; **training time, not data**, limits performance (big models were still improving at one week).

## Critique (Denny Britz)

D-softmax adds two hyperparameters with no analysis. More softmax baselines would help, since it's the simplest and needs no tuning.
