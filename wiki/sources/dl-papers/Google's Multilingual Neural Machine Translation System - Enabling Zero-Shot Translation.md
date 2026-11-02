---
type: source
title: "Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1611.04558"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - multilingual
  - transfer-learning
status: ingested
address: c-000248
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Multi-Way, Multilingual Neural Machine Translation with a Shared Attention Mechanism]]"
  - "[[Multi-Task Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/gnmt-multilingual.md]]"
---

# Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation

[Paper](https://arxiv.org/abs/1611.04558) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Johnson et al. take the unchanged GNMT architecture and prepend a **target-language token** (for example `<2fr>`) to the input. One model handles many-to-one, one-to-many and many-to-many translation. It does **zero-shot translation** between pairs never seen together (for example PT to ES via shared training on PT-EN and EN-ES), and shows evidence of a shared "interlingua" representation.

## Connections

The simplest possible multilingual design; the same trick (task tokens in the input) underlies T5 and instruction tuning. See [[Multi-Task Learning]].
