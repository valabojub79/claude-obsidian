---
type: source
title: "Character-Aware Neural Language Models"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1508.06615"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - language-modeling
  - character-level
status: ingested
address: c-000227
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Language Models and Sequence Generation]]"
  - "[[Training Very Deep Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/character-aware-nlm.md]]"
---

# Character-Aware Neural Language Models

[Paper](http://arxiv.org/abs/1508.06615) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Kim et al. feed an LSTM language model **character-CNN word representations** (via highway layers) instead of word embeddings. State of the art with far fewer parameters; it helps most on morphologically rich languages.

## Key points

- Small model: 15-d char embeddings, filters of width 1 to 6, 1 highway layer, 2-layer LSTM with 300 units, **5M parameters**. Large: widths 1 to 7, 2 highway layers, 650-ish units, 19M parameters. Hierarchical softmax.
- **Highway layers are essential**; an MLP instead doesn't work.
- Nearest neighbors after the highway layer are semantic; before it, orthographic.
- Adding word embeddings to the char features made results **worse**.

## Critique (Denny Britz)

This is really a way to learn word embeddings from characters. Could it be stacked for sentence representations? Why does an MLP fail so badly? Why only 15-d character embeddings?
