---
type: concept
title: "LISA Tutorial - 1D Segmentation of Cortical Layers"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - lasagne
  - segmentation
  - neuroscience
complexity: advanced
domain: deep-learning
status: developing
address: c-000164
related:
  - "[[Semantic Segmentation]]"
  - "[[Batch Normalization]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/cnn_1D_segm.txt]]"
---

# LISA Tutorial: 1D Segmentation (BigBrain Cortical Layers)

Segment the **6 layers of the cerebral cortex** in the BigBrain dataset (a 3D ultra-high-resolution brain reconstructed from 2D histology sections). Done in collaboration with Konrad Wagstyl (Cambridge).

## Turning 3D into 1D

Labeling whole 2D sections by hand is infeasible. Instead, sample **rays**: 200-pixel profiles running from outside the brain through the cortex. The cell-body stain intensity along a ray reflects cell density and size, which differ by layer, so boundaries show up as intensity changes.

- 2 input channels: smoothed and raw intensity.
- 7 labels: outside the cortex plus 6 layers.

## Model (simple beat complex)

8 identical **BN, ReLU, Conv1D** blocks (kernel **25**, 64 maps, "same" padding), then a 1x1 conv to 7 classes and per-pixel softmax.

- **No pooling**, so no upsampling path is needed; the output has the input's length.
- 8 layers of width-25 kernels give each output pixel a receptive field covering the **whole 200-pixel ray**, enough context.
- Fully convolutional, so any ray length works.

The authors tried more complex models first; this one had enough capacity.

## Results

Few mislabeled pixels per ray. Predicted rays were interpolated, smoothed and assembled into 3D meshes; intersected with 2D sections they matched ground truth closely and **generalized to previously unsegmented cortex**. Training took about 4 h on a Titan X.

Lesson: when the structure is inherently 1D (a depth profile), reframe the problem. It cuts labeling cost and model complexity.
