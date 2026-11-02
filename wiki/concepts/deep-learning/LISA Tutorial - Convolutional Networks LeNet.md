---
type: concept
title: "LISA Tutorial - Convolutional Networks LeNet"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - cnn
complexity: intermediate
domain: deep-learning
status: developing
address: c-000165
related:
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[Convolutional Neural Networks]]"
  - "[[Classic CNN Architectures]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/lenet.txt]]"
---

# LISA Tutorial: Convolutional Networks (LeNet)

A simplified LeNet-5 for MNIST in Theano. It complements DLAI's [[Convolutional Neural Networks]] with the biological motivation and implementation detail.

## Biological motivation

Hubel and Wiesel (1968): cat visual-cortex cells respond to small **receptive fields**. **Simple cells** detect edge-like patterns; **complex cells** have larger fields and are locally position-invariant. Models inspired by this: NeoCognitron, HMAX, LeNet-5.

## Two key ideas

- **Sparse connectivity**: each unit connects to a local patch of the layer below. Stacking layers grows the effective receptive field (3 then 5 then...), so features become increasingly global.
- **Shared weights**: one filter replicated across the image forms a **feature map**. The gradient of a shared weight is the **sum** of the gradients at every position. It detects features anywhere and cuts parameters drastically.

A feature map: `h^k_ij = tanh( (W^k * x)_ij + b_k )`. Layer weights form a 4D tensor `[out maps, in maps, filter h, filter w]`; input is `[batch, in maps, h, w]`.

Fun fact: a **randomly initialized** 9x9 filter already behaves like an edge detector.

## Max pooling

Non-overlapping regions output their max:

1. Cuts computation for upper layers.
2. Gives translation robustness. With 2x2 pooling after a conv, 3 of the 8 one-pixel shifts give identical output; with 3x3, 5 of 8.

## Architecture

Alternating `{conv + max-pool}` layers (`LeNetConvPoolLayer`) on 4D tensors, then flatten to 2D, then `HiddenLayer` (MLP), then `LogisticRegression`. Weight init uses fan-in = `in_maps * filter_h * filter_w`.

## Hyperparameter tips

- **Number of filters**: a conv filter costs `(M-m)(N-n) * m*n * K_{l-1}` per map, far more than an MLP unit, so use fewer filters than MLP units. Feature maps shrink with depth, so use **few filters near the input and more higher up**, keeping `#maps x #positions` roughly constant per layer, and the total activation count non-decreasing to preserve information.
- **Filter shape**: about 5x5 for 28x28 MNIST; 12x12 to 15x15 first-layer filters for large natural images. Pick the "granularity" that matches the scale of the abstractions.
- **Pooling**: 2x2 or none; 4x4 only for very large images in lower layers (it discards 15/16 of the signal).
- Also try PCA whitening and per-epoch learning-rate decay.
