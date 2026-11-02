---
type: concept
title: "Inception Network and 1x1 Convolutions"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
  - cnn
complexity: advanced
domain: deep-learning
status: developing
address: c-000162
related:
  - "[[Classic CNN Architectures]]"
  - "[[Residual Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Inception Network and 1x1 Convolutions

## 1x1 convolution ("Network in Network", Lin et al., 2013)

On a `6x6x32` volume, a `1x1x32` filter is a tiny fully connected layer applied at every pixel across channels, followed by ReLU.

- **Shrink channels**: `28x28x192` with 32 filters of 1x1 gives `28x28x32` (pooling shrinks H and W; 1x1 conv shrinks C).
- **Add non-linearity** while keeping C unchanged.
- LeCun: "In ConvNets there is no such thing as fully connected layers, only 1x1 convolutions with a full connection table."

## Inception module (Szegedy et al., 2014: "Going Deeper with Convolutions")

Instead of choosing a filter size, **do them all in parallel** and concatenate along channels:

```
input 28x28x192 -> [1x1 | 3x3 same | 5x5 same | maxpool same] -> concat 28x28x256
```

### The cost problem, and bottlenecks

A direct `5x5`, 32-filter conv on `28x28x192`: `28*28*32 * 5*5*192 ~ 120M` multiplies.

With a 1x1 **bottleneck** first (192 to 16 channels):

- `28*28*16 * 192 ~ 2.4M`
- `28*28*32 * 5*5*16 ~ 10M`
- Total **~12.4M**, a 10x cut, with no measurable loss in accuracy.

The full module puts 1x1 reductions before the 3x3 and 5x5 branches, and a 1x1 after the max-pool branch (to cut its 192 channels).

## GoogLeNet

Stacks of Inception modules, with occasional max-pools between them, plus two **auxiliary softmax heads** mid-network. These keep intermediate features predictive and have a regularizing effect. The name comes from the "we need to go deeper" meme.

Successors: Inception v2, v3, v4, and Inception-ResNet (combining with [[Residual Networks]]). The same depthwise-and-1x1 thinking led to MobileNet.
