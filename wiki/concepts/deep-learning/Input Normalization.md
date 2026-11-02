---
type: concept
title: "Input Normalization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: beginner
domain: deep-learning
status: developing
address: c-000163
related:
  - "[[Batch Normalization]]"
  - "[[Gradient Descent]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Input Normalization

Rescale input features to zero mean and unit variance before training:

```
mu    = (1/m) * sum x_i
X     = X - mu
sigma2 = (1/m) * sum x_i^2      (element-wise, after centering)
X     = X / sqrt(sigma2)
```

Compute `mu` and `sigma2` on the **training set** and apply the same values to the dev and test sets.

## Why

Features on very different scales (say 1 to 1000 vs 0 to 1) give an elongated, ravine-shaped cost surface, so gradient descent zig-zags and needs a tiny learning rate. Normalized features give a rounder bowl, which allows a larger learning rate and faster convergence. It never hurts, so do it by default.

[[Batch Normalization]] applies the same idea to every hidden layer.

## Related

Feature-scaling variants (min-max, standardization, robust scaling) are covered in [[ai-notes|AI-Notes]]: [[Feature Scaling]].
