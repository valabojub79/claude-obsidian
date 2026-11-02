---
type: concept
title: "DLAI Course 1 - Neural Networks and Deep Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - dlai-course
complexity: beginner
domain: deep-learning
status: developing
address: c-000139
related:
  - "[[deeplearning-ai-summary|DeepLearning.ai Summary]]"
  - "[[DLAI Course 2 - Improving Deep Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
---

# DLAI Course 1: Neural Networks and Deep Learning

First course of Andrew Ng's Deep Learning Specialization, as summarized in [[deeplearning-ai-summary|DeepLearning.ai Summary]]. Goal: build and train a fully connected deep network from scratch with vectorized NumPy.

## Why deep learning took off

Three drivers, in Ng's framing:

1. **Data.** Classic models (logistic regression, SVM) plateau as data grows; neural networks keep improving, and bigger networks improve more. Mobile and IoT keep feeding data.
2. **Compute.** GPUs, faster CPUs, distributed training, ASICs.
3. **Algorithms.** Example: replacing sigmoid with ReLU sped training up by avoiding vanishing gradients (see [[Activation Functions]]).

Supervised-learning network families: standard NN for structured (tabular) data, [[Convolutional Neural Networks|CNNs]] for images, [[Recurrent Neural Networks|RNNs]] for sequences such as audio and text, and hybrids.

## Course map

| Week | Topic | Wiki pages |
|------|-------|-----------|
| 1 | Introduction | this page |
| 2 | Neural network basics | [[Logistic Regression]], [[Gradient Descent]], [[Backpropagation]], [[Vectorization and Broadcasting]] |
| 3 | Shallow networks (one hidden layer) | [[Activation Functions]], [[Weight Initialization]] |
| 4 | Deep L-layer networks | [[Deep L-Layer Neural Network]], [[Parameters vs Hyperparameters]] |

## Build recipe

1. Define structure (input features, layer sizes, outputs).
2. Initialize parameters (random weights, zero biases).
3. Loop: forward pass and loss, backward pass for gradients, parameter update.

Start simple (logistic regression, then a shallow net) before going deep.

## Is it "like the brain"?

Ng calls the brain analogy oversimplified: a logistic unit loosely resembles a neuron, but nobody knows how biological neurons learn. Deep learning is best seen as a very flexible function approximator for X to Y mappings.

## Interview: Ian Goodfellow

Inventor of GANs (see [[Generative Adversarial Networks]]). Points: stabilizing GAN training is the key open problem; ML security should be designed in from the start, not patched later; publish code on GitHub to get noticed.
