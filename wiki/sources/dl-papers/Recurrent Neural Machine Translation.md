---
type: source
title: "Recurrent Neural Machine Translation"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1607.08725"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - attention
status: ingested
address: c-000283
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation with Recurrent Attention Modeling]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/recurrent-nmt.md]]"
---

# Recurrent Neural Machine Translation

[Paper](http://arxiv.org/abs/1607.08725) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Replace Bahdanau attention with a **recurrent (GRU) attention** to capture attention history and mitigate the **coverage** problem. Beats Moses and GroundHog on Chinese-English; attention-RNN activations visualize sensibly. Training: 2 weeks on a Titan X, 300 batches per hour, 2.9M pairs.

## Critique (Denny Britz)

The "dependencies among source states" argument is weak, since BiRNN states already encode them. Very slow for 2.9M pairs, so maybe impractical in production. Idea: use RL to cover source spans out of order. Moses isn't evaluated on long sentences.
