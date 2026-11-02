---
type: concept
title: "Ridge Regression"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regression
  - linear-models
  - regularization
complexity: intermediate
domain: machine-learning
status: developing
address: c-000370
related:
  - "[[Lasso Regression]]"
  - "[[Elastic Net Regression]]"
  - "[[Regularization in Machine Learning]]"
  - "[[Regularization]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Ridge Regression.md]]"
---

# Ridge Regression (L2)

[[Linear Regression]] plus an **L2 penalty**:

```
L = MSE + lambda * sum_i w_i^2
```

From [[ai-notes|AI-Notes]]; the same idea as weight decay in neural nets ([[Regularization]]).

## Effect of lambda

- As lambda grows, coefficients **shrink toward 0 but never become exactly 0** (the quadratic penalty's gradient vanishes near 0).
- **Large coefficients shrink most.**
- Higher lambda means higher bias and lower variance; lower lambda the reverse. See [[Bias Variance Tradeoff]].

## When to use

You already trust your feature set and just want to curb **overfitting**, especially with correlated features ([[Multicollinearity]]): ridge spreads weight across correlated features and stabilizes the solution (`X^T X + lambda I` is always invertible).

## Sensitivities

- **Outliers**: somewhat less damaging than plain OLS, because coefficients are restrained.
- **Scaling**: **required**. The penalty treats all coefficients equally, so feature units matter; scaling also speeds gradient descent ([[Feature Scaling]]).

Compare [[Lasso Regression]] (sparse) and [[Elastic Net Regression]] (both).
