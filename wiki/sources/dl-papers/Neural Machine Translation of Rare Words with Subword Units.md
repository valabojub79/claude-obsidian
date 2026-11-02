---
type: source
title: "Neural Machine Translation of Rare Words with Subword Units"
source_type: paper
year: 2015
url: "https://arxiv.org/abs/1508.07909"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - tokenization
status: ingested
address: c-000267
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Language Models and Sequence Generation]]"
  - "[[A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nmt-subword.md]]"
---

# Neural Machine Translation of Rare Words with Subword Units

[Paper](https://arxiv.org/abs/1508.07909) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Sennrich, Haddow and Birch adapt **Byte Pair Encoding (BPE)** to split rare words into subword units, giving open-vocabulary NMT without UNK replacement or back-off dictionaries. A significant BLEU gain over baselines.

## Algorithm

Start with a character vocabulary; repeatedly **merge the most frequent adjacent pair**. Final vocabulary = characters + number of merges (the hyperparameter). It's pure pre- and post-processing; the model is unchanged.

- **Joint BPE** (shared source and target) segments shared names identically, which eases alignment.
- Intuition: many words translate compositionally (stems, suffixes, compounds, transliterated names).
- Setup: Groundhog on top of Bahdanau attention; beam 12; Adadelta, batch 80; 60k separate or 90k joint vocabulary for EN-DE.

## Critique (Denny Britz)

60 to 90k seems large; would 20 to 30k suffice?

## Connections

BPE (and WordPiece and Unigram descendants) became **the** tokenization for GPT, BERT, T5 and essentially all LLMs. See [[Language Models and Sequence Generation]].
