---
type: concept
title: "Parameters vs Hyperparameters"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
complexity: beginner
domain: deep-learning
status: developing
address: c-000188
related:
  - "[[Hyperparameter Tuning]]"
  - "[[Deep L-Layer Neural Network]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
---

# Parameters vs Hyperparameters

- **Parameters** are learned by training: weights `W[l]` and biases `b[l]` (also BatchNorm's `gamma` and `beta`).
- **Hyperparameters** are chosen by you and control how the parameters get learned: learning rate `alpha`, number of iterations, number of layers `L`, units per layer `n[l]`, activation choice, and later momentum, mini-batch size, regularization strength and so on.

Deep learning is empirical: the right values depend on data, hardware and domain, and they drift over time, so revisit them. Systematic search is covered in [[Hyperparameter Tuning]].

Historically the learning rate was sometimes called a "parameter"; today everyone calls it a hyperparameter.
