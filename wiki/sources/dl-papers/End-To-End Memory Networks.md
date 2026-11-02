---
type: source
title: "End-To-End Memory Networks"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1503.08895"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - memory
  - reasoning
  - attention
status: ingested
address: c-000242
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Neural Turing Machines]]"
  - "[[Recurrent Memory Network for Language Modeling]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/end-to-end-memory-networks.md]]"
---

# End-To-End Memory Networks

[Paper](http://arxiv.org/abs/1503.08895) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Sukhbaatar et al. (MemN2N). Store input sentences in memory, then do **multiple attention hops** over them conditioned on the query, trained end to end with backprop (unlike the original Memory Networks, which needed supporting-fact supervision). Evaluated on bAbI QA and language modeling. Beats weakly supervised baselines but not the strongly supervised MemNN.

## Key points

- Sentence encoding: bag of words, or **position encoding** (PE).
- bAbI vocabulary about 180 words; 1k or 10k training examples.
- Essentially Bahdanau attention over sentences, with no output per step and a simpler score.

## Critique (Denny Britz)

The PE formula is unexplained; there are many tricks (jittering, linear start) and little intuition; the weight-tying constraints are unclear; LM gains are small and probably due to heavy tuning; no training cost is reported.

## Connections

Multi-hop attention over memory is close to stacked Transformer attention: query, key, value.
