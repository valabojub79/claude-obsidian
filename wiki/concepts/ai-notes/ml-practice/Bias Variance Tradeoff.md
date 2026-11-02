---
type: concept
title: "Bias Variance Tradeoff"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - ml-fundamentals
complexity: beginner
domain: machine-learning
status: developing
address: c-000374
related:
  - "[[Bias and Variance]]"
  - "[[Regularization in Machine Learning]]"
  - "[[Cross Validation]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Bias Variance Tradeoff.md]]"
---

# Bias-Variance Tradeoff

From [[ai-notes|AI-Notes]] (CampusX). The deep-learning-practice view is in [[Bias and Variance]] (DLAI).

- **Bias**: the model's inability to capture the true relationship (systematic error).
- **Variance**: how much the model's predictions change when the training data changes.

Classically they trade off: lowering one tends to raise the other.

| | Train performance | Test performance | Diagnosis | Fixes |
|-|------------------|------------------|-----------|-------|
| **Overfitting** | Great | Poor | Low bias, **high variance** | Regularization ([[Regularization in Machine Learning]]), more data, simpler model |
| **Underfitting** | Poor | Poor | **High bias**, low variance | More complex model, better features, train longer |

## Bias-variance decomposition (squared error)

```
E[(y - f_hat(x))^2] = Bias[f_hat(x)]^2 + Var[f_hat(x)] + sigma^2      # sigma^2 = irreducible noise
```

Bias is **squared** so that positive and negative deviations don't cancel, and so the terms add in the same units as MSE. The irreducible error is the noise floor: no model can beat it (compare **Bayes error** in [[Human-Level Performance]]).

DLAI's point: with big data and big regularized networks you can often reduce both, so the tradeoff is softer in deep learning.
