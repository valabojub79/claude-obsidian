---
type: source
title: "Incorporating Copying Mechanism in Sequence-to-Sequence Learning"
source_type: paper
year: 2016
url: "http://arxiv.org/abs/1603.06393"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - summarization
  - attention
status: ingested
address: c-000252
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Pointer Networks]]"
  - "[[Sequence to Sequence Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/copynet.md]]"
---

# Incorporating Copying Mechanism in Sequence-to-Sequence Learning

[Paper](http://arxiv.org/abs/1603.06393) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** **CopyNet** (Gu et al.) lets a seq2seq decoder either *generate* from the vocabulary or *copy* a token from the source. The output distribution mixes a generate mode and a copy mode (attention-like scores over source positions), so the effective vocabulary is the vocabulary plus the source words. It helps on toy copying tasks, summarization (LCSTS) and dialogue, especially with names and rare words.

## Connections

The copy idea from [[Pointer Networks]]; close relatives are [[Pointer Sentinel Mixture Models]] and pointer-generator networks for summarization.
