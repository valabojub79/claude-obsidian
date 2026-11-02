---
type: source
title: "A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1603.06147"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - character-level
status: ingested
address: c-000206
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation by Jointly Learning to Align and Translate]]"
  - "[[Neural Machine Translation of Rare Words with Subword Units]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/char-level-decoder.md]]"
---

# A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation

[Paper](http://arxiv.org/abs/1603.06147) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Chung, Cho and Bengio keep a **BPE subword encoder** but decode at the **character** level, with no explicit segmentation. Character decoding beats word-level decoding on WMT EN-DE, EN-CS, EN-RU and EN-FI. A proposed **bi-scale** decoder (slow and fast layers) helped little.

## Key points

- Builds on Bahdanau attention: BiRNN encoder with 512 units, 2-layer decoder with 1024 units, Adam, batch 128, gradient clipping at norm 1.
- Moses tokenizer; at most 50 source subwords; target at most 100 subwords or 500 characters.
- Attention plots show characters aligning cleanly with source subwords.

## Critique (Denny Britz)

Well written, with a rare table of run-to-run variance. Why no character-level **encoder**? Perhaps no time, or bad results. (A follow-up did it: [[Fully Character-Level Neural Machine Translation without Explicit Segmentation]].)
