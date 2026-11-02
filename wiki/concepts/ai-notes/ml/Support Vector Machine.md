---
type: concept
title: "Support Vector Machine"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - classification
  - kernels
complexity: advanced
domain: machine-learning
status: developing
address: c-000372
related:
  - "[[Logistic Regression]]"
  - "[[Hyperparameter Optimization]]"
  - "[[Feature Scaling]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Support Vector Machine.md]]"
---

# Support Vector Machine (SVM)

A maximum-margin classifier. From [[ai-notes|AI-Notes]] (CampusX mentorship notebooks).

- **Support vectors**: the training points closest to the boundary; they alone determine it.
- **Margin**: the distance between the boundary and the support vectors. Maximizing it makes the model robust to small data changes (lower variance).

## Hard-margin SVM (maximal margin classifier)

Maximize the margin subject to **no violations**: every point correctly classified and outside the margin. Solved by quadratic programming.

- Requires **perfectly linearly separable** data.
- One outlier can become a support vector and force a tiny margin, which overfits.
- **Prediction**: plug `x` into `w.x + b`; positive gives the positive class.
- **Multiclass**: One-vs-Rest (K binary SVMs; take the most confident). One-vs-One is another option.

## Soft-margin SVM

Allow violations, measured by **slack variables** `xi_i`:

| `xi` | Meaning |
|------|---------|
| 0 | Correct and outside the margin |
| (0, 1) | Inside the margin, still correct |
| 1 | Exactly on the boundary |
| > 1 | Misclassified |

```
minimize  1/2 ||w||^2 + C * sum_i xi_i
```

**C** trades margin width against violations. **High C** punishes violations, giving a narrow margin and overfitting. **Low C** gives a wide margin, more violations, and underfitting. Tune C on a log grid (`1e-3 ... 1e3`) with cross-validation ([[Hyperparameter Optimization]]).

## Kernels and the kernel trick

Soft margin is still linear. **Kernels** implicitly map data into a higher-dimensional space where it becomes linearly separable. Common kernels: **linear**, **polynomial**, **RBF** (Gaussian), **sigmoid**.

The **kernel trick**: the SVM dual depends on data only through inner products, so replace `x_i . x_j` with `K(x_i, x_j)` and never compute the high-dimensional mapping explicitly. It's a "trick" because you get the effect of the transformation for the cost of a kernel evaluation.

## Practical

**Scale features** (margins are distance-based; see [[Feature Scaling]]). The RBF kernel's `gamma` and `C` interact, so tune them jointly. Uses: text classification (linear SVM), small and medium image tasks (pre-deep learning).

> [!gap] Unfinished in source
> The kernel-hyperparameter and applications questions are listed without answers.
