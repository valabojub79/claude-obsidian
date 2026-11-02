---
type: concept
title: "Feature Scaling"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - feature-engineering
  - preprocessing
complexity: beginner
domain: machine-learning
status: developing
address: c-000377
related:
  - "[[Input Normalization]]"
  - "[[K Nearest Neighbors]]"
  - "[[Gradient Descent]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Feature Scaling.md]]"
---

# Feature Scaling

Put features on comparable scales. From [[ai-notes|AI-Notes]]. The deep-learning version is [[Input Normalization]].

**Why**: (1) distance-based models ([[K Nearest Neighbors]], k-means, SVM) shouldn't be dominated by large-unit features; (2) [[Gradient Descent]] converges much faster on scaled features.

## Techniques

| Method | Formula | Result | Use when |
|--------|---------|--------|----------|
| **Standardization** (z-score) | `(x - mu) / sigma` | mean 0, std 1 | Gradient-based models, PCA, unbounded features |
| **Min-max normalization** | `(x - min) / (max - min)` | [0, 1] | Naturally bounded data (percentages, pixels), some neural nets; sensitive to outliers |
| **Robust scaling** | `(x - median) / IQR` | Centered, outlier-resistant | Data with [[Outliers]] |

(Max-abs scaling to [-1, 1] keeps sparse data sparse.) Tree models don't need scaling.

## fit vs transform

- `fit`: learn the statistics (mu, sigma, min, max) **on the training set only**.
- `transform`: apply them.
- `fit_transform`: both, on training data.

Then **only `transform`** the validation and test sets. Fitting on all data leaks test information.
