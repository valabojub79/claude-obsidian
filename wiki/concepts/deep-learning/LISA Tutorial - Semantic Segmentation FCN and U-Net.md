---
type: concept
title: "LISA Tutorial - Semantic Segmentation FCN and U-Net"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - lasagne
  - segmentation
  - medical-imaging
complexity: advanced
domain: deep-learning
status: developing
address: c-000176
related:
  - "[[Semantic Segmentation]]"
  - "[[Residual Networks]]"
  - "[[Data Augmentation]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/fcn_2D_segm.txt]]"
---

# LISA Tutorial: FCN and U-Net for Medical Image Segmentation

Two tutorials (`fcn_2D_segm`, `unet`), implemented in Theano + **Lasagne**, with data loaded via `fvisin/dataset_loaders`. Python 2. Concepts: [[Semantic Segmentation]].

## FCN-8 on colonoscopy polyps

**Data**: 912 frames from 36 patients, split **by patient** (train 20 patients / 547 frames, valid 8 / 183, test 8 / 182). Two classes (polyp, background). Random-crop augmentation also makes images equal-sized for batch > 1; validation and test run at batch size 1.

**FCN variants** (shared VGG-style downsampling path up to `conv7`):

| Variant | Upsampling path | Output detail |
|---------|-----------------|---------------|
| FCN-32 | conv7, then transposed conv with stride 32 | Coarse |
| FCN-16 | 2x up(conv7) + pool4, then stride 16 | Finer |
| FCN-8 | 2x up(2x up(conv7) + pool4) + pool3, then stride 8 | Finest (used here) |

Metrics: per-pixel accuracy and per-class **Jaccard (IoU)**. About 3.5 h on a Titan X; a second run took 6.5 h with different numbers, so **training variance is notable**.

Paper: Long, Shelhamer, Darrell, *Fully Convolutional Networks for Semantic Segmentation* (CVPR 2015); Vazquez et al. 2016 (endoluminal benchmark).

## U-Net on ISBI electron-microscopy stacks

Ronneberger, Fischer, Brox 2015. Compared with FCN-8:

1. **Symmetric** encoder and decoder, so many feature maps in the upsampling path (FCN keeps only `#classes` maps there).
2. Skip connections **concatenate** (cropped) encoder maps instead of summing them.

**Structure:**

- **Contracting**: 4 blocks of `[3x3 conv + BN + act] x2 -> 2x2 max-pool`; channels 64, 128, 256, 512.
- **Bottleneck**: 2 convs + BN, with **dropout**.
- **Expanding**: 4 blocks of `2x deconv -> concat skip -> [3x3 conv + BN + act] x2`.
- Output: 1x1 conv to `#classes`.

Why it suits biomedicine: it combines context with localization, takes any input size, and works with few annotated images given **heavy augmentation**. About 60 minutes on a Titan X.

## Legacy

U-Net remains the default for medical segmentation (nnU-Net), and its encoder-decoder-with-skips shape is the backbone of image **diffusion models**.
