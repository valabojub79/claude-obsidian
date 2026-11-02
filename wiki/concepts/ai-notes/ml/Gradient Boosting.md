---
type: concept
title: "Gradient Boosting"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - ensemble
  - boosting
complexity: advanced
domain: machine-learning
status: developing
address: c-000362
related:
  - "[[Ensemble Learning]]"
  - "[[Decision Tree]]"
  - "[[Gradient Descent]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Ensemble Learning/Gradient Boosting.md]]"
---

# Gradient Boosting

**Boosting**: train weak learners **sequentially**, each correcting the ensemble's current mistakes. Gradient boosting does this with **additive modeling** guided by the gradient of any differentiable loss. From [[ai-notes|AI-Notes]] (CampusX notebooks). Implementations: scikit-learn GBM, **XGBoost**, **LightGBM**, **CatBoost**.

Weak, high-bias learners (shallow trees) are chosen on purpose: fast, and resistant to overfitting individually.

## Algorithm (regression)

1. **Initialize** `F_0(x)` as a constant minimizing the loss (the target **mean** for squared error).
2. For `m = 1..M`:
   1. **Pseudo-residuals** `r_i = -dL(y_i, F(x_i)) / dF(x_i)`. For MSE this is simply `y_i - F_{m-1}(x_i)`, "the previous model's mistakes".
   2. Fit a small tree `h_m` to the residuals, which defines **terminal regions** (leaves).
   3. Compute the optimal output value per leaf (for MSE, the mean residual of the points in that leaf).
   4. Update `F_m(x) = F_{m-1}(x) + nu * h_m(x)`, with **learning rate** (shrinkage) `nu`.

## Function space vs parameter space

[[Gradient Descent]] moves **parameters** along the negative gradient. Gradient boosting moves the **function** itself: each new tree is a step along the negative gradient in function space. Hyperparameters (number of trees, depth, `nu`, subsampling) are then tuned in the usual way.

## Practical knobs

Number of estimators, `learning_rate` (smaller needs more trees but generalizes better), `max_depth` (3 to 8), `subsample` (stochastic gradient boosting), early stopping on a validation set.

> [!gap] Unfinished in source
> "Difference between gradient descent and gradient boosting" is an empty heading; the answer above is the standard one. Classification (log-loss) and XGBoost or CatBoost specifics aren't covered.
