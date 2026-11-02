---
type: source
title: "Fully Character-Level Neural Machine Translation without Explicit Segmentation"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.03017"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - character-level
  - cnn
status: ingested
address: c-000246
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation]]"
  - "[[Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/conv-char-level-nmt.md]]"
---

# Fully Character-Level Neural Machine Translation without Explicit Segmentation

[Paper](https://arxiv.org/abs/1610.03017) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Lee, Cho and Hofmann build char-to-char NMT. A **convolutional encoder** (embedding, conv, max-pool with stride, highway, BiGRU) shortens the source so attention is affordable; a 2-layer GRU decoder. Results on WMT'15 DE, CS, FI and RU to EN, bilingual and **multilingual** (one model, no language ID).

## Key points

- Character sequences are long and attention is quadratic, so **shrinking the source length is key**.
- Characters avoid OOV words and softmax blow-up, handle morphology, and scale to many languages without growing the model.
- char2char matches or beats bpe2char and bpe2bpe bilingually, and beats bpe2char multilingually. Robust to misspellings and unseen morphology.
- About 2 weeks on one Titan X (about 2.5 updates/s at batch 64).

## Critique (Denny Britz)

Could segmentation be read out of the trained network?
