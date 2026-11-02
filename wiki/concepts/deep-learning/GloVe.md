---
type: concept
title: "GloVe"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - embeddings
complexity: advanced
domain: deep-learning
status: developing
address: c-000157
related:
  - "[[Word Embeddings]]"
  - "[[Word2Vec and Negative Sampling]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# GloVe (Global Vectors)

Pennington, Socher, Manning, 2014. Learns embeddings directly from global co-occurrence counts.

`X_ij` is the number of times word `j` appears in the context of word `i` (symmetric if a symmetric window is used). Minimize:

```
sum_i sum_j f(X_ij) * ( theta_i . e_j + b_i + b'_j - log X_ij )^2
```

- `f(X_ij) = 0` when `X_ij = 0`, which sidesteps `log 0`.
- `f` caps the weight of very frequent words (the, is, of) while not under-weighting rare ones.
- `theta` and `e` play symmetric roles; the final embedding is often `(e_w + theta_w) / 2`.

The simplest of the classic algorithms. Less used than [[Word2Vec and Negative Sampling]], but popular for its simplicity and widely available pretrained vectors (6B, 42B, 840B tokens).

## Caveat

No guarantee that embedding axes align with interpretable features: the model is invariant to any invertible linear transform of the space.
