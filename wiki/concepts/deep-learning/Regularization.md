---
type: concept
title: "Regularization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - regularization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000190
related:
  - "[[Dropout]]"
  - "[[Data Augmentation]]"
  - "[[Bias and Variance]]"
  - "[[Batch Normalization]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Regularization

Techniques that reduce **variance** (overfitting), usually at a small cost in training fit.

## L2 regularization (weight decay)

```
J = (1/m) * sum L(y_hat, y) + (lambda / 2m) * sum_l ||W[l]||_F^2
dW[l] = (from backprop) + (lambda / m) * W[l]
W[l] := (1 - alpha*lambda/m) * W[l] - alpha * (from backprop)
```

The `(1 - alpha*lambda/m)` factor shrinks weights every step, hence "weight decay". The matrix norm is the **Frobenius norm** (sum of squared entries). `lambda` is a hyperparameter tuned on the dev set.

**L1** (`sum |w|`) drives many weights to exactly zero (sparse, smaller model), but L2 is far more common in deep learning.

### Why it works

- Large `lambda` pushes many weights near zero, so the network behaves like a smaller, simpler one.
- With tanh, small weights keep `z` in the near-linear region, so each layer is roughly linear and the whole function is smoother.
- Too large `lambda` over-smooths, giving high bias.

Debugging tip: plot the **regularized** `J`; it should fall monotonically.

## Other techniques

- [[Dropout]]: randomly drop units during training.
- [[Data Augmentation]]: synthesize more training examples.
- **Early stopping**: stop when dev error starts rising. It needs no extra hyperparameter, but Ng prefers L2 because early stopping couples "optimize J" and "don't overfit" into one knob, which breaks [[Orthogonalization]].
- **Ensembles**: train several models and average them. Often worth around 2%, at the cost of compute.
- [[Batch Normalization]] has a slight regularizing side effect; don't rely on it.

## In other sources

- Classical view: [[Ridge Regression]], [[Lasso Regression]], [[Elastic Net Regression]], [[Regularization in Machine Learning]].
