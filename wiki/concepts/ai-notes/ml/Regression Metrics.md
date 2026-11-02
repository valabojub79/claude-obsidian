---
type: concept
title: "Regression Metrics"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - evaluation
  - regression
complexity: beginner
domain: machine-learning
status: developing
address: c-000369
related:
  - "[[Classification Metrics]]"
  - "[[Linear Regression]]"
  - "[[Regression Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Performance Metrics/Regression Metrics.md]]"
---

# Regression Metrics

From [[ai-notes|AI-Notes]].

| Metric | Formula | Units | Notes |
|--------|---------|-------|-------|
| **MAE** | `mean |y - y_hat|` | Target units | Robust to outliers; not differentiable at 0 (subgradients still work) |
| **MSE** | `mean (y - y_hat)^2` | Squared units | Smooth, so the standard loss; **outlier-sensitive** |
| **RMSE** | `sqrt(MSE)` | Target units | Interpretable; still weights large errors more than MAE |
| **R^2** | `1 - SS_res / SS_tot` | Unitless | Compares against predicting the mean |
| **Adjusted R^2** | `1 - (1 - R^2)(n - 1)/(n - k - 1)` | Unitless | Penalizes extra features |

## R^2 (coefficient of determination, "goodness of fit")

- 1: perfect fit. 0: no better than the mean line. **Negative**: worse than the mean (a badly wrong model).
- Range is `(-inf, 1]`. (The source says "-1 to 1" and writes the formula as `(1 - SSE_r)/SSE_m`; the correct form is above.)
- **Flaw**: R^2 never decreases when you add features, even useless ones, because the model can always fit a bit more noise. **Adjusted R^2** fixes this by penalizing the number of predictors `k`.

Context-free (unitless) R^2 complements the context-dependent MAE, MSE and RMSE. Huber loss blends MSE and MAE (see [[Activation Functions]] for the deep-learning loss notes).

Statistical treatment: [[Regression Analysis]].
