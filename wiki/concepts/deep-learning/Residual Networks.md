---
type: concept
title: "Residual Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
  - cnn
complexity: intermediate
domain: deep-learning
status: developing
address: c-000191
related:
  - "[[Classic CNN Architectures]]"
  - "[[Vanishing and Exploding Gradients]]"
  - "[[Deep Residual Learning for Image Recognition]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Residual Networks (ResNets)

He et al., 2015. Very deep "plain" networks get **worse** training error as depth grows, because of vanishing and exploding gradients and harder optimization. ResNets fix this with **skip connections**.

## Residual block

```
a[l+1] = g(W[l+1] a[l] + b[l+1])
a[l+2] = g(W[l+2] a[l+1] + b[l+2] + a[l])      # shortcut added before the 2nd ReLU
```

## Why it works

If regularization drives `W[l+2]` and `b[l+2]` toward 0, then `a[l+2] = g(a[l]) = a[l]` (ReLU, `a >= 0`). The block can trivially learn the **identity**, so adding blocks rarely hurts, and any useful residual is a bonus. The shortcut also gives gradients a direct path backward. Training error keeps falling with depth.

## Dimensions

`z[l+2]` and `a[l]` must have the same shape, so blocks use "same" convolutions. When the shape changes, project with `W_s a[l]` (learned, or zero-padding).

## Block types (Keras assignment)

- **Identity block**: input and output shapes match; `CONV -> BN -> ReLU` twice (or three times) plus the shortcut.
- **Convolutional block**: the shortcut has a `CONV + BN` to change shape, and can use 1x1 bottlenecks.

## ResNet-34 / 50 / 152 design rules

All 3x3 convs are "same"; halving spatial size doubles the filter count; no FC hidden layers; no dropout; global average pool then softmax.

## Related

- Paper page: [[Deep Residual Learning for Image Recognition]].
- Skip connections reappear in Transformers ([[Transformer Architecture]]) and U-Net.
