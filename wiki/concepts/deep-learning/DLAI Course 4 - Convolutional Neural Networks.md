---
type: concept
title: "DLAI Course 4 - Convolutional Neural Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - dlai-course
  - computer-vision
complexity: intermediate
domain: deep-learning
status: developing
address: c-000142
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
  - "[[DLAI Course 5 - Sequence Models]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# DLAI Course 4: Convolutional Neural Networks

Computer vision with deep learning, as summarized in [[deeplearning-ai-summary|DeepLearning.ai Summary]].

## Course map

| Week | Topic | Wiki pages |
|------|-------|-----------|
| 1 | Foundations | [[Convolutional Neural Networks]] (convolution, padding, stride, pooling, LeNet-style network) |
| 2 | Case studies | [[Classic CNN Architectures]] (LeNet-5, AlexNet, VGG), [[Residual Networks]], [[Inception Network and 1x1 Convolutions]], [[Transfer Learning]], [[Data Augmentation]] |
| 3 | Object detection | [[Object Detection]] (localization, landmarks, sliding windows, YOLO, IoU, NMS, anchors, R-CNN family) |
| 4 | Special applications | [[Face Recognition]], [[Neural Style Transfer]] |

## State of computer vision (2017 view)

- Lots of data leads to simpler algorithms and less hand-engineering; little data leads to more "hacks" and careful architecture design.
- Speech has a lot of data, image classification a medium amount, object detection little. That is why detection architectures look complex.
- Two sources of knowledge: labeled data, and hand-engineered features, architectures and components. [[Transfer Learning]] helps when labeled data is scarce.

### Benchmark and competition tricks (rarely used in production)

- **Ensembling**: train 3 to 15 networks independently and average outputs; about 1 to 2% better, but N times slower.
- **Multi-crop at test time**: for example 10-crop. Classify several crops and average.

### Practical advice

Use architectures from the literature, use open-source implementations, start from pretrained weights and fine-tune.

## Extras: Keras

Create, compile (`optimizer`, `loss`, `metrics`), fit, evaluate. `model.summary()` prints layer shapes and parameter counts. It ran on TensorFlow, Theano or CNTK backends in 2017; today it is `tf.keras` / Keras 3.

## 1D and 3D convolutions

The same math applies to 1D signals (ECG, audio: `(14,1)` with 16 filters of size 5 gives `(10,16)`) and 3D volumes (CT scans, video). For 1D sequences, RNNs were more common in 2017 (see [[Recurrent Neural Networks]]).
