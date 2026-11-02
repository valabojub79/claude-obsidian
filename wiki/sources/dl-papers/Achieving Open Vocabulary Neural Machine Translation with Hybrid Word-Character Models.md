---
type: source
title: "Achieving Open Vocabulary Neural Machine Translation with Hybrid Word-Character Models"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1604.00788"
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
address: c-000215
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Neural Machine Translation of Rare Words with Subword Units]]"
  - "[[Fully Character-Level Neural Machine Translation without Explicit Segmentation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/open-vocab-nmt-hybrid-word-character.md]]"
---

# Achieving Open Vocabulary Neural Machine Translation with Hybrid Word-Character Models

[Paper](http://arxiv.org/abs/1604.00788) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Luong and Manning build a fast **word-level** NMT where `<unk>` tokens are handled by **character-level RNNs**. On the source side a char-RNN builds representations for rare words; on the target side, after producing `<unk>`, a char-RNN spells the word out. New state of the art: **19.9 BLEU** on WMT'15 English-Czech.

## Key points

- Source char-RNNs start from a zero state (allows pretraining); the final state is the word vector.
- Target char-RNN initialized from the word-RNN state ("same-path") or a separate representation ("separate-path").
- **Attention is critical** for pure character-based NMT.

## Critique (Denny Britz)

With more compute, would pure character models win, making hybrids a detour?
