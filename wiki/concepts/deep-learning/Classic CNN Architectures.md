---
type: concept
title: "Classic CNN Architectures"
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
address: c-000137
related:
  - "[[Convolutional Neural Networks]]"
  - "[[Residual Networks]]"
  - "[[Inception Network and 1x1 Convolutions]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Classic CNN Architectures

Reading case studies is the fastest way to learn how to combine conv, pool and FC layers. Architectures that work on one task often transfer to others.

## LeNet-5 (LeCun et al., 1998)

- Handwritten digits, `32x32x1` grayscale input.
- `CONV(5x5, 6) -> POOL -> CONV(5x5, 16) -> POOL -> FC 120 -> FC 84 -> output 10`.
- About **60k** parameters. Used sigmoid and tanh, plus average pooling. Modern versions use ReLU and max pooling.
- Established the "shrink H and W, grow channels" pattern.

## AlexNet (Krizhevsky, Sutskever, Hinton, 2012)

- ImageNet, 1000 classes, `227x227x3` input.
- `CONV 11x11 s4 -> MAXPOOL -> CONV 5x5 same -> MAXPOOL -> CONV 3x3 x3 -> MAXPOOL -> FC 4096 -> FC 4096 -> softmax 1000`.
- About **60M** parameters, with **ReLU**. Trained across 2 GPUs. Its Local Response Normalization was later shown to add little.
- Convinced the computer-vision community that deep learning works. Paper: *ImageNet Classification with Deep Convolutional Neural Networks* (no detailed note in the paper repo).

## VGG-16 (Simonyan & Zisserman, 2015)

- Radical simplicity: **only** `CONV 3x3, s=1, same` and `MAXPOOL 2x2, s=2`.
- Channels double per stage: 64, 128, 256, 512, 512. Pooling alone does the shrinking.
- About **138M** parameters (mostly FC); about 96 MB of activations per image for the forward pass.
- VGG-19 is larger but not much better.

## Later landmarks

- [[Residual Networks]] (ResNet, 2015): skip connections enable 152+ layers.
- [[Inception Network and 1x1 Convolutions]] (GoogLeNet, 2014): parallel filter sizes, 1x1 bottlenecks.
- Network-in-Network (2013): introduced 1x1 convolutions.

## Use open source

Papers omit details (learning-rate decay, tuning). Start from an author's GitHub implementation **with pretrained weights**, then apply [[Transfer Learning]].
