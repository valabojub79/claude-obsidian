---
type: concept
title: "Object Detection"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
complexity: advanced
domain: deep-learning
status: developing
address: c-000185
related:
  - "[[Convolutional Neural Networks]]"
  - "[[DLAI Course 4 - Convolutional Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Research Papers/Computer Vision/Object Detection Notes.md]]"
---

# Object Detection

## Task ladder

| Task | Output |
|------|--------|
| Classification | One label per image |
| Classification + localization | Label plus one bounding box |
| Detection | Label plus box for **every** object |
| Semantic segmentation | Label per pixel (instances merged) |
| Instance segmentation | Label per pixel, instances separated |

## Localization target

```
y = [p_c, b_x, b_y, b_h, b_w, c_1, ..., c_k]
```

`p_c` says whether there is an object. If `p_c = 0`, the rest are "don't care" and only `p_c` enters the loss. In practice: logistic loss for `p_c`, softmax log-loss for classes, squared error for the box.

**Landmark detection** outputs key points instead (64 face landmarks, skeleton joints). Landmark order must be consistent across all labels.

## Sliding windows, done convolutionally

Naive: crop windows at many scales and run a classifier on each, which is very slow. **OverFeat** (Sermanet 2014): turn FC layers into convolutions (a `5x5x16` input with 400 `5x5` filters is "FC 400"). Then one forward pass over the whole image yields a grid of predictions that shares computation across windows. Weakness: box positions are coarse.

## YOLO ("You Only Look Once", Redmon 2015)

1. Put an `S x S` grid on the image (for example 19x19).
2. Each object is assigned to the cell containing its **midpoint**; `b_x, b_y` are relative to that cell (0 to 1); `b_h, b_w` may exceed 1.
3. One convolutional pass outputs `S x S x (anchors * (5 + classes))`.

Fast, and it sees global context, but it is weaker on small objects.

### Intersection over Union

`IoU = area(intersection) / area(union)`. "Correct" usually means `IoU >= 0.5`.

### Non-max suppression (per class)

1. Drop boxes with `p_c < 0.6`.
2. Repeat: keep the highest-`p_c` box; discard remaining boxes with `IoU > 0.5` against it.

### Anchor boxes

Let one cell predict several objects of different shapes (tall pedestrian, wide car). Each object is assigned to (midpoint cell, anchor with highest IoU). Choose anchors by hand (5 to 10 shapes) or by k-means on the training boxes. YOLOv2 (YOLO9000) on a `608x608` input gives `19x19x5x85` (5 anchors, 80 classes): about 51M parameters.

## Region proposals (R-CNN family)

| Model | Idea | Speed |
|-------|------|-------|
| R-CNN (Girshick 2013) | Segmentation proposes about 2,000 regions; classify each | Slow |
| Fast R-CNN (2015) | Conv sliding window classifies all proposals at once | Faster |
| Faster R-CNN (Ren 2016) | A CNN (RPN) proposes regions too | Still slower than YOLO |
| Mask R-CNN (2017) | Adds a mask head (instance segmentation) | |

Other single-shot detectors: SSD, MultiBox; R-FCN is a more efficient Faster R-CNN. Ng prefers the single-pass idea.

## Related

- Paper notes on detection: see [[deeplearning-papernotes|Deep Learning Paper Notes]].
- Segmentation from scratch in Theano: [[LISA Tutorial - Semantic Segmentation FCN and U-Net]].

## AI-Notes perspective: R-CNN and selective search

[[ai-notes|AI-Notes]]' research notes on detection (CNN, R-CNN, Fast and Faster R-CNN, YOLO, with YOLO v1 to v8 planned):

- **Detection vs classification**: localize (bounding box) *and* classify every object.
- A plain CNN can localize **one** object (box regression plus class head). Many objects need sliding windows, which is expensive, with a window-size trade-off between accuracy and speed.
- Alternatives: **region proposals** (R-CNN family) vs **single-shot** detectors (SSD, YOLO with anchors and feature pyramids).

### Selective search (R-CNN's proposal step, about 2,000 regions)

1. **Over-segment** the image into small regions by low-level cues (color).
2. **Similarity-based merging**: color, texture, size similarity.
3. **Hierarchical**: repeatedly merge the most similar adjacent pair, then recompute similarities.
4. **Stop** at a target region count or minimum size.

Regions are **warped** to the CNN's fixed input size. Weakness: each of about 2,000 regions goes through the CNN separately, which is slow. That's what Fast and Faster R-CNN fix.

The note also lists **privacy masking** for detected regions (number plates): bitwise-AND masks, pixelation, Gaussian blur, mosaic, dithering, watermarking.
