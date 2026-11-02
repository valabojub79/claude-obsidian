---
type: source
title: "Generating Sentences from a Continuous Space"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1511.06349"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - vae
  - generative
status: ingested
address: c-000247
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Autoencoders]]"
  - "[[Language Models and Sequence Generation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/generating-sentences-cont-space.md]]"
---

# Generating Sentences from a Continuous Space

[Paper](http://arxiv.org/abs/1511.06349) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Bowman et al.'s **RNN variational autoencoder** for sentences. An encoder maps the sentence to a Gaussian latent `z`, and the decoder RNN generates from `z`. Loss = reconstruction + KL to the prior.

## Key points

- **Posterior collapse:** naive training lets the decoder ignore `z` and the KL term falls to 0.
- Fix 1, **KL cost annealing**: ramp the KL weight from 0 to 1.
- Fix 2, **word dropout**: replace decoder inputs with UNK at some rate, forcing reliance on `z`.
- LM: the standard VAE slightly trails an RNNLM; with an input-less decoder it wins. Imputation of missing words is much better than RNNLM (the comparison is somewhat unfair).
- Interpolating in latent space yields grammatical, meaningful sentences; more word dropout gives more diverse samples.

## Connections

[[Autoencoders]]; posterior collapse remains a classic VAE-for-text problem.
