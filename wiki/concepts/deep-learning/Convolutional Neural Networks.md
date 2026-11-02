---
type: concept
title: "Convolutional Neural Networks"
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
address: c-000138
related:
  - "[[DLAI Course 4 - Convolutional Neural Networks]]"
  - "[[Classic CNN Architectures]]"
  - "[[LISA Tutorial - Convolutional Networks LeNet]]"
  - "[[Object Detection]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Vision/Convolutional Neural Nets.md]]"
---

# Convolutional Neural Networks

Networks built from **convolution**, **pooling** and **fully connected** layers, designed for grid data such as images.

## Why not fully connected?

A `1000x1000x3` image has 3M inputs. A dense layer of 1,000 units would need 3 **billion** weights. Convolutions fix this with:

1. **Parameter sharing**: a feature detector (say a vertical-edge filter) useful in one place is useful everywhere.
2. **Sparse connections**: each output depends on a small patch only. This also gives translation robustness.

## The convolution operation

Slide an `f x f` filter over the image, taking elementwise products and summing. Example: the vertical edge filter `[[1,0,-1],[1,0,-1],[1,0,-1]]` fires on a bright-to-dark vertical boundary. Hand-crafted variants: **Sobel** `[[1,0,-1],[2,0,-2],[1,0,-1]]`, **Scharr** `[[3,0,-3],[10,0,-10],[3,0,-3]]`. In deep learning the 9 numbers are **learned**.

Strictly, deep learning "convolution" is **cross-correlation** (no filter flip); the flip doesn't matter when weights are learned.

## Output size

```
n_out = floor( (n + 2p - f) / s ) + 1
```

- **Padding** `p`: without it, outputs shrink and border pixels are underused. "Valid" means `p = 0`; "same" means `p = (f-1)/2` when `s = 1`.
- **Stride** `s`: jump `s` pixels per step.
- `f` is usually odd (3, 5, 7): symmetric padding and a center pixel.

## Volumes and multiple filters

An `n x n x n_c` input needs `f x f x n_c` filters. Each filter gives one 2D map; `n_c'` filters stack to `n_out x n_out x n_c'`.

One conv layer: `A[l] = ReLU(conv(A[l-1], W[l]) + b[l])`. Parameters: `f*f*n_c[l-1]*n_c[l] + n_c[l]`. Example: 10 filters of `3x3x3` give 280 parameters, **independent of image size**, so convolutions are less prone to overfitting.

## Pooling

- **Max pooling** (`f=2, s=2` is typical): keeps the strongest response in each window and halves height and width. No learnable parameters.
- **Average pooling**: rarer, mostly to collapse a final `7x7x1000` to `1x1x1000`.
- Padding is rarely used in pooling.

## Typical pattern

```
CONV -> POOL -> CONV -> POOL -> FC -> FC -> SOFTMAX
```

Height and width shrink while channels grow. FC layers hold most of the parameters; early conv layers use most of the memory. Borrow hyperparameters from published architectures ([[Classic CNN Architectures]]).

## Related

- From-scratch Theano implementation: [[LISA Tutorial - Convolutional Networks LeNet]].
- AI-Notes perspective: see the section below.
- Paper notes: CV entries in [[deeplearning-papernotes|Deep Learning Paper Notes]].

## AI-Notes perspective (interview Q&A)

[[ai-notes|AI-Notes]] (from DLAI Course 4 and CampusX):

- **Why not an ANN for images?** Flattening explodes parameter count and **destroys spatial information** (pixel neighborhoods encode texture, shape and structure).
- **Why not an RNN?** Same compute and spatial issues. But **CNN + RNN** works for video: the CNN encodes frames and the RNN models time (activity recognition).
- **Layers**: convolution (feature extractor; early layers find edges, deep layers find shapes), non-linearity, **pooling** (downsample, memory, translation invariance), then flatten or global pooling, then a fully connected **classification head**.
- **Parametric vs not**: conv layers learn weights; pooling layers have **no parameters**.
- **Pooling types**: max (keeps the strongest response), average (smooth summary), **global** max or average (one value per map, size-independent), fractional (non-integer ratios), strided.
- **Pooling drawbacks**: discards information, and its translation invariance **hurts segmentation**, where location matters (see [[Semantic Segmentation]]).
- Grayscale has 1 channel; RGB has 3, so filters span all channels.

> [!contradiction] Edge filters
> AI-Notes calls Sobel the "vertical" filter and Scharr the "horizontal" one. Both Sobel and Scharr come in vertical **and** horizontal versions; Scharr just weights the center row or column more heavily (3, 10, 3 instead of 1, 2, 1). See the convolution section above. The source's feature-map formula is also garbled; the correct form is `floor((n + 2p - f)/s) + 1`.
