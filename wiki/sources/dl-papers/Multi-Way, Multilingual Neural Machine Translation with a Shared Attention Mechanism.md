---
type: source
title: "Multi-Way, Multilingual Neural Machine Translation with a Shared Attention Mechanism"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1601.01073"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - multilingual
status: ingested
address: c-000261
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation]]"
  - "[[Multi-task Sequence to Sequence Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/multi-way-nmt-shared-attention.md]]"
---

# Multi-Way, Multilingual Neural Machine Translation with a Shared Attention Mechanism

[Paper](http://arxiv.org/abs/1601.01073) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Firat, Cho and Bengio build **one** NMT model for N x M language pairs, with per-language encoders and decoders and a **single shared attention** mechanism. Parameters grow linearly, not quadratically, with languages. Biggest gains for **low-resource** pairs.

## Key points

- Encoders and decoders emit attention-specific vectors that are combined, so adding a language doesn't multiply parameters.
- BiRNN encoders, 620-d embeddings, GRUs with 1k units; Adam, batch 60, sentences up to 50 words.
- Large-data pairs gain little. The model doesn't fit on one GPU. Zero-shot was possible in principle but not evaluated.
- Difference from [[Multi-task Sequence to Sequence Learning]]: the shared attention.

## Critique (Denny Britz)

Nothing forces encoders into a shared representation; they may encode language-specific cues for the decoders.
