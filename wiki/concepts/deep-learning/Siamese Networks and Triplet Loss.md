---
type: concept
title: "Siamese Networks and Triplet Loss"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - metric-learning
complexity: advanced
domain: deep-learning
status: developing
address: c-000194
related:
  - "[[Face Recognition]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Siamese Networks and Triplet Loss

## Siamese network

Two (or three) copies of the **same** network with **shared weights** encode inputs into embeddings; a distance between embeddings decides similarity. Train it so `||f(x1) - f(x2)||^2` is small for matching pairs and large otherwise.

## Triplet loss

Compare an **Anchor** to a **Positive** (same identity) and a **Negative** (different identity):

```
||f(A) - f(P)||^2 + alpha <= ||f(A) - f(N)||^2

L(A, P, N) = max( ||f(A)-f(P)||^2 - ||f(A)-f(N)||^2 + alpha, 0 )
J = sum over triplets L(A_i, P_i, N_i)
```

- The **margin** `alpha` prevents the trivial solution where every embedding is equal (or zero).
- Needs several examples per identity during training (not at deployment).

## Hard triplet mining

Random triplets are too easy (`d(A,N)` is usually already large), so nothing is learned. Choose triplets where `d(A,P)` is close to `d(A,N)`. FaceNet's paper details the strategy.

## Uses beyond faces

Signature verification, image retrieval, few-shot learning, and sentence embeddings (Siamese BERT). Contrastive and InfoNCE losses in modern self-supervised learning are close relatives.
