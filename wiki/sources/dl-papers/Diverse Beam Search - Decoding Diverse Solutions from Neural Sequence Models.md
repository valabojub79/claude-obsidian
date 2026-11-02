---
type: source
title: "Diverse Beam Search - Decoding Diverse Solutions from Neural Sequence Models"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.02424"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - decoding
  - sequence-models
status: ingested
address: c-000237
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Beam Search]]"
  - "[[A Diversity-Promoting Objective Function for Neural Conversation Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/diverse-beam-search.md]]"
---

# Diverse Beam Search - Decoding Diverse Solutions from Neural Sequence Models

[Paper](https://arxiv.org/abs/1610.02424) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Split a beam of width `B` into `G` groups of `B/G`. Run beam search per group in sequence, adding a **dissimilarity penalty** (weight `lambda`) against tokens chosen by earlier groups at the same step. Outputs are much more diverse than standard beam search (which yields near-duplicates), at little cost, for image captioning, MT and visual question generation.

## Connections

Fixes a known weakness of [[Beam Search]]; an alternative to MMI reranking ([[A Diversity-Promoting Objective Function for Neural Conversation Models]]).
