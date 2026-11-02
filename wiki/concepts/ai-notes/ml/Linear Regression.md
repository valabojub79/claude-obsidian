---
type: concept
title: "Linear Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regression
  - linear-models
complexity: beginner
domain: machine-learning
status: developing
address: c-000365
related:
  - "[[Ridge Regression]]"
  - "[[Lasso Regression]]"
  - "[[Polynomial Regression]]"
  - "[[Gradient Descent]]"
  - "[[Regression Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Linear Regression.md]]"
---

# Linear Regression

Estimate a **linear relationship** between a target and its features: `y = b0 + b1 x1 + ... + bn xn`. From [[ai-notes|AI-Notes]] (CampusX). *Linear* refers to the relationship being linear (in the parameters); *regression* to studying the strength and reliability of that relationship.

- **Simple** linear regression: one feature. **Multiple**: several.
- **Parametric**: it makes assumptions about the data, and the parameter count (slopes plus intercept) doesn't grow with the data.
  - **Slope** `w_i`: change in `y` per unit change in `x_i`.
  - **Intercept**: the baseline output when the features are 0.

## Finding the best-fit line (plane, hyperplane)

The line minimizing the cost (MSE).

1. **Ordinary least squares (OLS)**: closed form `w = (X^T X)^{-1} X^T y`. Matrix inversion costs `O(n^3)` in the number of features, and it **fails under perfect multicollinearity** (`X^T X` is singular). See [[Multicollinearity]].
2. **[[Gradient Descent]]**: iterative; scales to many features and samples.

## Sensitivities

- **Scaling**: matters for gradient descent convergence; see [[Feature Scaling]].
- **Outliers**: very sensitive; squared error amplifies them and can lead to overfitting. Use [[Regularization in Machine Learning|regularization]] ([[Ridge Regression]], [[Lasso Regression]], [[Elastic Net Regression]]) or robust losses; see [[Outliers]].
- **Missing values**: can't handle them; impute first ([[Missing Values]]).

## Bias and variance

Fitting outliers and noise without regularization gives low bias and high variance. Too few or uninformative features give high bias, which you fix with feature engineering or more data. See [[Bias Variance Tradeoff]].

## Open questions in the source

Why MSE? (Answer: it's the maximum-likelihood estimate under Gaussian noise; convex and differentiable.) The classic **assumptions** (linearity, independence of errors, homoscedasticity, normal errors, no perfect multicollinearity) are listed but not filled in; see [[Regression Analysis]] for the statistics view.
