---
type: source
title: "Dual Learning for Machine Translation"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1611.00179"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - reinforcement-learning
  - semi-supervised
status: ingested
address: c-000239
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation with Reconstruction]]"
  - "[[Learning to Translate in Real-time with Neural Machine Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/dual-learning-mt.md]]"
---

# Dual Learning for Machine Translation

[Paper](https://arxiv.org/abs/1611.00179) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** He et al. use **monolingual** data through a two-agent "dual game" trained with policy gradient:

1. Translate a French sentence to English.
2. Reward 1: an English language model scores fluency.
3. Translate it back to French.
4. Reward 2: `log P(original | translation)` scores reconstruction.

Total reward is a linear combination; samples come from beam search.

## Results (BLEU, before then after dual learning)

| Direction | 100% parallel data | 10% parallel data |
|-----------|-------------------|-------------------|
| EN to FR | 29.92 to 32.06 | 25.73 to 28.73 |
| FR to EN | 27.49 to 29.78 | 22.27 to **27.50** |

With 10% of the parallel data plus monolingual fine-tuning, it approaches full-data systems.

## Critique (Denny Britz)

Very promising; training from monolingual data **only** would be amazing, but RL variance makes that hard. The rewards are noisy (neither an LM nor BLEU measures correctness). Why the large jump for FR to EN with 10% data but not EN to FR?

## Connections

The same round-trip idea as back-translation and CycleGAN.
