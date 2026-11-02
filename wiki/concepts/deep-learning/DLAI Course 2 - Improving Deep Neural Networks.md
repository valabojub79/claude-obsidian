---
type: concept
title: "DLAI Course 2 - Improving Deep Neural Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - dlai-course
complexity: intermediate
domain: deep-learning
status: developing
address: c-000140
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[DLAI Course 1 - Neural Networks and Deep Learning]]"
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# DLAI Course 2: Improving Deep Neural Networks

Full title: *Hyperparameter Tuning, Regularization and Optimization*. Second course of the specialization ([[deeplearning-ai-summary|DeepLearning.ai Summary]]). It turns the from-scratch network of Course 1 into something that trains reliably and fast.

## Course map

| Week | Topic | Wiki pages |
|------|-------|-----------|
| 1 | Practical aspects | [[Train Dev Test Split]], [[Bias and Variance]], [[Regularization]], [[Dropout]], [[Data Augmentation]], [[Input Normalization]], [[Vanishing and Exploding Gradients]], [[Weight Initialization]], [[Gradient Checking]] |
| 2 | Optimization algorithms | [[Mini-Batch Gradient Descent]], [[Optimization Algorithms]] (EWA, momentum, RMSprop, Adam, learning-rate decay) |
| 3 | Tuning, BatchNorm, frameworks | [[Hyperparameter Tuning]], [[Batch Normalization]], [[Softmax Regression]], [[Deep Learning Frameworks]] |

## Core message

Applied deep learning is an iterative `idea -> code -> experiment` loop. Go round it faster by:

- splitting data well and reading bias and variance off train and dev error,
- using the "basic recipe": fix high bias with a bigger network or longer training; fix high variance with more data or regularization,
- picking good defaults (He init, Adam, BatchNorm, a log-scale learning-rate search).

In the deep learning era the old bias/variance *tradeoff* matters less: a bigger network lowers bias without raising variance much (given regularization), and more data lowers variance without raising bias. "Training a bigger network almost never hurts."

## Extras

- For good papers, read the ICLR and NeurIPS proceedings.
- Interview: Yuanqing Lin (Baidu Research, PaddlePaddle, an early ImageNet winner).
