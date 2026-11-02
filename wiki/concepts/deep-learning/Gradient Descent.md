---
type: concept
title: "Gradient Descent"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: beginner
domain: deep-learning
status: developing
address: c-000159
related:
  - "[[Optimization Algorithms]]"
  - "[[Backpropagation]]"
  - "[[Logistic Regression]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/1- Neural Networks and Deep Learning/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Machine Learning/Optimization Algorithms/Gradient Descent.md]]"
---

# Gradient Descent

Iteratively move parameters a small step against the gradient of the cost:

```
w := w - alpha * dJ/dw
b := b - alpha * dJ/db
```

`alpha` is the **learning rate**, usually the single most important hyperparameter (see [[Parameters vs Hyperparameters]]).

## Intuition

- The derivative is the slope: nudging `a` by `0.001` in `f(a) = 3a` changes `f` by `0.003`.
- For non-linear `f`, the slope depends on where you are, which is why the derivative is itself a function.
- Each step is greedy: it follows the locally steepest downhill direction.

## Practical notes from DLAI

- Normalizing inputs makes the cost surface rounder, so descent converges faster (see [[Input Normalization]]).
- Full-batch descent on large datasets is slow. [[Mini-Batch Gradient Descent]] and the momentum-style methods in [[Optimization Algorithms]] are the standard fixes.
- Gradients come from [[Backpropagation]]; verify them with [[Gradient Checking]].

## AI-Notes perspective

[[ai-notes|AI-Notes]] adds the classical-ML framing:

- **Gradient** = the vector of partial derivatives, pointing toward steepest **increase**, so step the opposite way: `new = old - lr * dL/dw`.
- **Convex vs non-convex**: one global minimum (linear and logistic regression) vs many local minima and saddle points (neural nets).
- **Stopping**: a fixed number of epochs, or when parameter change falls below a threshold.
- **Learning rate**: too high overshoots or diverges; too low is slow.
- **Variants**: **batch** (whole dataset per update: stable but slow), **stochastic** (one random point per update: fast but jumpy), **mini-batch** (the compromise; see [[Mini-Batch Gradient Descent]]).
