---
type: concept
title: "Decision Tree"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - trees
  - classification
  - regression
complexity: intermediate
domain: machine-learning
status: developing
address: c-000359
related:
  - "[[Random Forest]]"
  - "[[Ensemble Learning]]"
  - "[[Feature Selection]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Tree Based Models/Decision Tree.md]]"
---

# Decision Tree

A supervised model for classification **and** regression: a learned, nested if/else structure. From [[ai-notes|AI-Notes]] (CampusX).

- **White box**: every prediction comes with its decision path, which makes trees excellent for explanation.
- **Non-parametric**: no assumptions about the data distribution; the structure (number of nodes) grows with the data.

## Algorithms

| | CART | ID3 | C4.5 |
|-|------|-----|------|
| Tree shape | Binary | Multi-way | Multi-way |
| Split criterion | Gini (classification), variance/MSE (regression) | Information gain (entropy) | Gain ratio |

scikit-learn uses (an optimized) **CART**.

## Splitting (classification)

```
Gini(node) = 1 - sum_k p_k^2
Entropy(node) = - sum_k p_k log2 p_k
Split score = (n_left/n) * G_left + (n_right/n) * G_right       # pick the minimum
```

- Numeric feature: sort the values; candidate thresholds are the midpoints between consecutive values.
- Categorical with more than 2 levels (CART): one-vs-rest groupings.
- **Gini vs entropy**: nearly always give similar trees; Gini is cheaper (no log). Ranges: Gini `[0, 1 - 1/K]` (0 to 0.5 for binary); entropy `[0, log2 K]` (0 to 1 for binary).

**Regression**: choose splits that most reduce **variance (MSE)**; leaves predict the mean.

## Overfitting and pruning

Defaults grow until leaves are pure (or have zero variance), giving low bias and very high variance. Regularize by **pruning**:

- **Pre-pruning** (early stopping): `max_depth`, `min_samples_split`, `min_samples_leaf`, `min_impurity_decrease`, `max_leaf_nodes`, `max_features` (rule of thumb `sqrt(F)` or `log2(F)`). Risk: short-sightedness (a poor split now might enable great ones later).
- **Post-pruning**: grow fully, then remove weak subtrees (scikit-learn: cost-complexity pruning, `ccp_alpha`). Better, but costlier.

## Quirks

- **Axis-aligned splits**: rotate the data 45 degrees and the boundary becomes a staircase that generalizes worse. PCA or rotation can help.
- **Complexity**: training roughly `O(F * N log N)` per level; prediction is `O(depth)`, about `O(log N)` if balanced and `O(N)` worst case.
- **Feature importance**: total impurity reduction per feature, which can drive [[Feature Selection]].

Trees are the base learners of [[Random Forest]] and [[Gradient Boosting]].
