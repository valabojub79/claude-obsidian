---
type: concept
title: "Semantic Segmentation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
  - segmentation
complexity: intermediate
domain: deep-learning
status: developing
address: c-000192
related:
  - "[[LISA Tutorial - Semantic Segmentation FCN and U-Net]]"
  - "[[Object Detection]]"
  - "[[Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/fcn_2D_segm.txt]]"
---

# Semantic Segmentation

Predict a class for **every pixel**. Classification needs *what*; segmentation needs *what* and *where*. Instance segmentation additionally separates objects of the same class (see the task ladder in [[Object Detection]]).

## Fully convolutional design

Only locally connected layers (convolution, pooling, upsampling), **no dense layers**. That means fewer parameters and any input size works. Two paths:

- **Downsampling (encoder)**: captures context, the *what*.
- **Upsampling (decoder)**: recovers resolution, the *where*. Uses **transposed convolutions** ("deconvolution") or unpooling.
- **Skip connections** bring fine spatial detail from the encoder into the decoder, by sum (FCN) or concatenation (U-Net).

Architectures: FCN-32/16/8 (Long et al. 2015), U-Net (Ronneberger 2015), later SegNet, DeepLab (atrous convolution), Mask R-CNN (instance), SAM (promptable).

## Metrics

- **Pixel accuracy**: correct pixels divided by all pixels. Misleading under class imbalance (background dominates).
- **Jaccard / IoU per class**: `|P inter GT| / |P union GT|`; mean IoU over classes is standard. Dice `2|P inter GT| / (|P| + |GT|)` is common in medical imaging.

## 1D segmentation

The same machinery works on signals: [[LISA Tutorial - 1D Segmentation of Cortical Layers]].

Implementations: [[LISA Tutorial - Semantic Segmentation FCN and U-Net]].
