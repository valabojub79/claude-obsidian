---
type: source
title: "Grammar as a Foreign Language"
source_type: paper
year: 2014
url: "http://arxiv.org/abs/1412.7449"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - parsing
  - sequence-models
status: ingested
address: c-000249
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence to Sequence Models]]"
  - "[[Attention Mechanism]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/grammar-as-a-foreign-language.md]]"
---

# Grammar as a Foreign Language

[Paper](http://arxiv.org/abs/1412.7449) (2014) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Vinyals et al. treat **constituency parsing as translation**: a 3-layer seq2seq LSTM (256 units) with attention outputs the linearized parse tree. New state of the art.

## Results

- WSJ only (40k sentences): 90.5 F1. **Attention matters a lot here.**
- Plus about 11M sentences auto-parsed by existing parsers (and 90k gold): **92.8**. The student **beats its teacher parsers**, perhaps because their errors look like noise to the LSTM.

## Key points

- Handles about 70-token sentences without degrading.
- Reversing the input gave only +0.2; pretrained word vectors only +0.4.
- Big lesson: existing models can label large datasets that train a better model.

## Critique (Denny Britz)

Does the tree linearization (DFS with parentheses) matter? Does auto-label noise put a ceiling on accuracy? Why not a BiLSTM?
