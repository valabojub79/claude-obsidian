---
type: source
title: "DeepLearning.ai Summary"
source_type: repository
author: "Mahmoud Badry"
date_published: 2018-01-01
date_ingested: 2026-11-02
created: 2026-11-02
updated: 2026-11-02
url: "https://github.com/mbadry1/DeepLearning.ai-Summary"
commit: ccf3287c9a2598092df5adb03925781988df903e
license: MIT
confidence: high
tags:
  - source
  - deep-learning
  - course-notes
status: ingested
address: c-000124
related:
  - "[[DLAI Course 1 - Neural Networks and Deep Learning]]"
  - "[[DLAI Course 2 - Improving Deep Neural Networks]]"
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
  - "[[DLAI Course 4 - Convolutional Neural Networks]]"
  - "[[DLAI Course 5 - Sequence Models]]"
  - "[[Andrew Ng]]"
  - "[[Deep Learning]]"
sources:
  - ".raw/repos/DeepLearning.ai-Summary/"
key_claims:
  - "Deep learning took off because of data scale, compute, and algorithmic advances such as ReLU"
  - "Diagnose with bias and variance relative to human-level error before choosing a fix"
  - "Adam, He initialization and batch norm are robust defaults"
  - "Attention removes the fixed-length bottleneck of encoder-decoder RNNs"
---

# DeepLearning.ai Summary (mbadry1)

Mahmoud Badry's 2017-2018 notes on Andrew Ng's five-course **Deep Learning Specialization** (Coursera, deeplearning.ai). It's one Markdown README per course, about 260 KB of text plus diagrams. MIT licensed. Snapshot at commit `ccf3287`, stored locally (gitignored) in `.raw/repos/DeepLearning.ai-Summary/`.

## Course pages

1. [[DLAI Course 1 - Neural Networks and Deep Learning]]: logistic regression to deep L-layer nets, vectorized.
2. [[DLAI Course 2 - Improving Deep Neural Networks]]: regularization, initialization, optimizers, BatchNorm, tuning.
3. [[DLAI Course 3 - Structuring Machine Learning Projects]]: ML strategy, error analysis, data mismatch.
4. [[DLAI Course 4 - Convolutional Neural Networks]]: CNNs, case studies, detection, faces, style transfer.
5. [[DLAI Course 5 - Sequence Models]]: RNNs, LSTM, GRU, embeddings, seq2seq, attention, speech.

## Pages created by this ingest (50)

Course 1: [[Logistic Regression]], [[Gradient Descent]], [[Backpropagation]], [[Vectorization and Broadcasting]], [[Activation Functions]], [[Deep L-Layer Neural Network]], [[Parameters vs Hyperparameters]]

Course 2: [[Train Dev Test Split]], [[Bias and Variance]], [[Regularization]], [[Dropout]], [[Data Augmentation]], [[Input Normalization]], [[Vanishing and Exploding Gradients]], [[Weight Initialization]], [[Gradient Checking]], [[Mini-Batch Gradient Descent]], [[Optimization Algorithms]], [[Hyperparameter Tuning]], [[Batch Normalization]], [[Softmax Regression]], [[Deep Learning Frameworks]]

Course 3: [[Orthogonalization]], [[Evaluation Metrics and Dev Sets]], [[Human-Level Performance]], [[Error Analysis]], [[Data Mismatch]], [[Transfer Learning]], [[Multi-Task Learning]], [[End-to-End Deep Learning]]

Course 4: [[Convolutional Neural Networks]], [[Classic CNN Architectures]], [[Residual Networks]], [[Inception Network and 1x1 Convolutions]], [[Object Detection]], [[Face Recognition]], [[Siamese Networks and Triplet Loss]], [[Neural Style Transfer]]

Course 5: [[Recurrent Neural Networks]], [[Language Models and Sequence Generation]], [[Gated Recurrent Unit]], [[Long Short-Term Memory]], [[Word Embeddings]], [[Word2Vec and Negative Sampling]], [[GloVe]], [[Sequence to Sequence Models]], [[Beam Search]], [[BLEU Score]], [[Attention Mechanism]], [[Speech Recognition and CTC]]

## Reliability notes

> [!stale] Dated in places
> Written in 2017-2018: TensorFlow 1.x code (sessions, placeholders), no Transformers, and "state of the art" claims (YOLOv2, Faster R-CNN) that have since been superseded. The concepts remain the standard foundation.

- A few small errors in the source were corrected in the wiki pages: the variance in input normalization should be computed after centering, and divided by its square root; BatchNorm `gamma` and `beta` have shape `(n[l], 1)`, not `(n[l], m)`; the "high bias and variance" example compares train with dev, not test.
- Extra resources the repo links: Tess Ferrandez's sketch notes; review posts by Ryan Shrott and Arthur Chan.
