---
type: source
title: "Latent Predictor Networks for Code Generation"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1603.06744"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - code-generation
  - attention
status: ingested
address: c-000254
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Pointer Networks]]"
  - "[[Incorporating Copying Mechanism in Sequence-to-Sequence Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/latent-predictor-networks.md]]"
---

# Latent Predictor Networks for Code Generation

[Paper](http://arxiv.org/abs/1603.06744) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Ling et al. generate code from **multiple predictors**: attention-based character generation plus **pointer networks** that copy tokens from the input, with the choice of predictor treated as a latent variable and marginalized during training. The task is to generate the Python or Java implementation of a **Magic: The Gathering** or **Hearthstone** card from its text fields. Clearly beats seq2seq and attention baselines.

## Connections

An early neural code-generation benchmark, ancestor of today's code LLMs; it combines copy and generate like [[Incorporating Copying Mechanism in Sequence-to-Sequence Learning|CopyNet]].
