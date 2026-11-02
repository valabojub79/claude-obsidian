---
type: concept
title: "Elastic Net Regression"
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
address: c-000360
related:
  - "[[Ridge Regression]]"
  - "[[Lasso Regression]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Linear Models/Elastic Net Regression.md]]"
---

# Elastic Net Regression

A middle ground between [[Ridge Regression]] and [[Lasso Regression]]: add **both** penalties to the linear-regression cost. From [[ai-notes|AI-Notes]].

```
L = MSE + alpha * ( l1_ratio * sum|w| + (1 - l1_ratio)/2 * sum w^2 )      # scikit-learn form
```

- `l1_ratio = 0`: pure L2 (ridge). `l1_ratio = 1`: pure L1 (lasso). `0 <= l1_ratio <= 1` is a tuning knob, along with overall strength `alpha`.
- Use it when you can't decide between ridge and lasso, or when you have **groups of correlated features** (lasso alone picks one at random; elastic net keeps the group).
- Fit by [[Gradient Descent]] or coordinate descent; scale features first.
