---
type: concept
title: "Data Augmentation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - regularization
  - computer-vision
complexity: beginner
domain: deep-learning
status: developing
address: c-000144
related:
  - "[[Regularization]]"
  - "[[Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Data Augmentation

Create extra training examples by applying label-preserving transformations. It's a cheap way to get "more data" and reduce variance.

## Image transformations

- Mirroring (horizontal flip).
- Random cropping.
- Rotation, shearing, local warping.
- **Color shifting**: add random offsets to RGB channels; AlexNet's PCA color augmentation does this along the principal components.
- For OCR: random rotations and distortions of characters.

Augmented examples are not as good as truly independent new data, but they are nearly free.

## Implementation (DLAI Course 4)

A common pattern: CPU threads load and distort images while the GPU trains on the previous batch, so augmentation adds no wall-clock cost.

## Related

- Part of the [[Regularization]] toolbox.
- Used with [[Transfer Learning]] when data is scarce.
- Artificial data synthesis for speech and vision can help with [[Data Mismatch]], but beware overfitting to a small synthetic subset.
