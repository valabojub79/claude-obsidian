---
type: concept
title: "Face Recognition"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
  - metric-learning
complexity: advanced
domain: deep-learning
status: developing
address: c-000154
related:
  - "[[Convolutional Neural Networks]]"
  - "[[End-to-End Deep Learning]]"
  - "[[Siamese Networks and Triplet Loss]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Face Recognition

## Verification vs recognition

- **Verification** (1:1): given an image and a claimed ID, is it that person?
- **Recognition** (1:K): given an image, which of K people is it (or none)? It needs a very accurate verifier (99.9%+), because errors compound over K comparisons.
- **Liveness detection** stops a photo of a face from fooling the system; it can be learned with supervised data.

## One-shot learning

You may have **one** photo per employee, and new people join constantly, so a softmax over K people doesn't work. Instead learn a **similarity function**:

```
d(img1, img2) <= tau   =>  same person
```

Implemented with [[Siamese Networks and Triplet Loss]]: the same CNN encodes each face to an embedding `f(x)` (for example 128-d), and `d = ||f(x1) - f(x2)||^2`.

## Training options

1. **Triplet loss** (FaceNet, Schroff 2015). Needs several photos per person in the training set (commercial systems use 10M to 100M images), with **hard** triplets.
2. **Binary classification** (DeepFace, Taigman 2014): feed the pair through the Siamese CNN, then `y_hat = sigmoid( sum_k w_k |f(x_i)_k - f(x_j)_k| + b )`. Chi-square distance is an alternative.

## Deployment trick

Precompute and store the embeddings of all database faces; at query time encode only the new face.

## Pipeline vs end-to-end

The best 2017 systems were **two-step**: detect and crop the face, then compare embeddings. Each step has abundant data. See [[End-to-End Deep Learning]].
