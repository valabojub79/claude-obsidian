---
type: source
title: "A Structured Self-Attentive Sentence Embedding"
source_type: paper
year: 2017
url: "https://arxiv.org/abs/1703.03130"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - attention
  - embeddings
status: ingested
address: c-000213
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Attention Mechanism]]"
  - "[[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/self_attention_embedding.md]]"
---

# A Structured Self-Attentive Sentence Embedding

[Paper](https://arxiv.org/abs/1703.03130) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Lin et al. (IBM and MILA) represent a sentence as a **matrix**: a BiLSTM's states `H`, combined by `r` different attention distributions:

```
A = softmax(W_s2 tanh(W_s1 H^T))        # r x n, one row per "view"
M = A H                                  # sentence embedding, r x 2u
P = || A A^T - I ||_F^2                  # penalty: rows should attend to different parts
```

Beats other sentence encoders on author profiling, sentiment and textual entailment; the attention rows make embeddings easy to **visualize**. Both the penalty and multiple rows matter empirically.

## Critique (Denny Britz)

"Multi-hop" is a misnomer: it's one hop with several independent attentions (multi-head, effectively). Nice hyperparameter analysis; some datasets oddly subsampled. Could extend to NMT. Simple but cool.

## Connections

Multi-row attention closely anticipates the Transformer's **multi-head attention**.
