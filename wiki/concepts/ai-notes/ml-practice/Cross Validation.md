---
type: concept
title: "Cross Validation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - model-evaluation
complexity: beginner
domain: machine-learning
status: developing
address: c-000376
related:
  - "[[Train Dev Test Split]]"
  - "[[Hyperparameter Optimization]]"
  - "[[Imbalanced Data]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Cross Validation.md]]"
---

# Cross Validation

A **resampling** technique (alongside the bootstrap) for estimating how a model performs on unseen data, and how much that estimate **varies**. From [[ai-notes|AI-Notes]].

## Hold-out method

Single train/test split (`train_test_split`). Simple and cheap, but:

1. **Wastes data**: the test part is never used for training.
2. **High variability**: results change with the random split (`random_state`).

## K-fold CV

Split the data into `k` folds; train on `k-1`, test on 1; rotate `k` times; average the metric. It reduces variability, at `k` times the cost.

| Variant | How | Pros and cons |
|---------|-----|---------------|
| **LOOCV** | k = n (one point per test fold) | Very expensive; high-variance estimate (each test is one point, outliers dominate); bad under imbalance; can't compute R^2 on one point |
| **K-fold** | k = 5 or 10 | Cheaper, lower variance; but a fold may miss the minority class |
| **Stratified K-fold** | Each fold keeps the class proportions | Default for classification, especially imbalanced data ([[Imbalanced Data]]) |
| **Repeated K-fold** | Repeat with different shuffles | More stable estimate |
| **Nested CV** | Inner loop tunes, outer loop evaluates | Unbiased estimate when tuning hyperparameters |
| (Time series) | Forward-chaining splits | Never train on the future |

## Train, validation, test

- **Train**: fit parameters.
- **Validation**: tune hyperparameters and select models.
- **Test**: final, untouched estimate. **Never tune on the test set**: that leaks information and inflates scores (see [[Hyperparameter Optimization]]).

Typical split: 80/10/10 or 70/15/15 for modest data. With millions of examples DLAI recommends 98/1/1 ([[Train Dev Test Split]]).
