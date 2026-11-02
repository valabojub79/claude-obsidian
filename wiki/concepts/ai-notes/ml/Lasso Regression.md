---
type: concept
title: "Lasso Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regression
  - linear-models
  - regularization
  - feature-selection
complexity: intermediate
domain: machine-learning
status: developing
address: c-000364
related:
  - "[[Ridge Regression]]"
  - "[[Elastic Net Regression]]"
  - "[[Feature Selection]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Lasso Regression.md]]"
---

# Lasso Regression (L1)

[[Linear Regression]] plus an **L1 penalty**:

```
L = MSE + lambda * sum_i |w_i|
```

From [[ai-notes|AI-Notes]].

## Sparsity

As lambda grows, coefficients shrink and **some become exactly 0**. The L1 penalty's constant-magnitude gradient pushes small weights all the way to zero (geometrically, the L1 ball has corners on the axes). Zeroed features are effectively removed, so the model is **sparse**. That's built-in **feature selection**.

## Bias and variance

High lambda means more zeros, less predictive power, high bias and low variance; low lambda the reverse.

## When to use

You're unsure which features matter, or have **high-dimensional** data and want the important predictors identified automatically. See [[Feature Selection]].

Caveats: with groups of **correlated** features, lasso tends to pick one arbitrarily, in which case [[Elastic Net Regression]] is better. Scale features first ([[Feature Scaling]]).

> [!note] Source quirk
> The AI-Notes "sensitivity to outliers" paragraph here is copied from the ridge page (it says "in ridge regression"). The same reasoning applies: regularized coefficients reduce outlier influence somewhat.
