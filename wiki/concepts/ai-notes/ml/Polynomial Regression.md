---
type: concept
title: "Polynomial Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regression
  - linear-models
  - feature-engineering
complexity: beginner
domain: machine-learning
status: developing
address: c-000367
related:
  - "[[Linear Regression]]"
  - "[[Bias Variance Tradeoff]]"
  - "[[Hyperparameter Optimization]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Polynomial Regression.md]]"
---

# Polynomial Regression

For curved relationships, where plain [[Linear Regression]] underfits: generate **polynomial features** up to degree `d`, then fit a linear model on them. From [[ai-notes|AI-Notes]].

## Features generated

With `x1, x2` and `d = 2`, `PolynomialFeatures` produces `1, x1, x2, x1^2, x2^2, x1*x2`, including **interaction** terms. The count of terms (with bias) for `n` features and degree `d` is the binomial coefficient `C(n + d, d)`, so it grows fast. `d = 0` leaves only the bias, which underfits badly.

## Why it's still "linear"

Linear means linear **in the parameters**: `y = b0 + b1 x + b2 x^2 + e` is a linear combination of the `b`s, even though it's curved in `x`.

## Choosing the degree

- Too high: fits noise (low bias, high variance).
- Too low: underfits.
- Tune `d` with [[Hyperparameter Optimization]] and [[Cross Validation]].

## Practical notes

- Fit with [[Gradient Descent]] (OLS's matrix inversion is costly with many polynomial terms).
- **Scale features**: `x^3` and `x^4` explode in magnitude ([[Feature Scaling]]).
- **Outliers** are amplified by high powers, so handle them first ([[Outliers]]).
- Polynomial terms are **highly correlated** with each other, the same [[Multicollinearity]] issues as linear regression (unstable coefficients, high standard errors). Regularize ([[Ridge Regression]]).
