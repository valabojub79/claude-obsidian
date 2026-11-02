---
type: concept
title: "Principal Component Analysis"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - unsupervised
  - dimensionality-reduction
complexity: intermediate
domain: machine-learning
status: developing
address: c-000405
related:
  - "[[Feature Selection]]"
  - "[[Multicollinearity]]"
  - "[[K Nearest Neighbors]]"
  - "[[Autoencoders]]"
sources:
  - "[[.raw/repos/AI-Notes/Unsupervised Learning/Dimensionality Reduction Techniques/PCA.md]]"
---

# Principal Component Analysis (PCA)

Unsupervised **feature extraction**: rotate the data onto new orthogonal axes (**principal components**) ordered by variance, then keep the top few. From [[ai-notes|AI-Notes]] (CampusX, Krish Naik).

## Why: the curse of dimensionality

Past some number of features, performance **degrades**: data becomes sparse, distances lose meaning ([[K Nearest Neighbors]]), and compute and overfitting grow. Two remedies: **select** features ([[Feature Selection]]) or **extract** new ones (PCA, [[Autoencoders]]).

## Prerequisites

Variance, covariance, matrices as linear transformations, vector projection, eigenvalues and eigenvectors.

## Why variance?

Maximizing spread along the kept components retains the most information. Variance (not mean absolute deviation) because it's differentiable and algebraically convenient: it leads to the covariance-eigenvector solution.

## Algorithm

1. **Mean-center** the data (and usually standardize; see [[Feature Scaling]]). The source calls centering optional, but covariance-based PCA always centers; without it the first component just points at the mean.
2. Compute the **covariance matrix** `C = X^T X / (n - 1)`: the variance of each feature, plus how pairs of features co-vary.
3. **Eigendecompose** `C`. Eigenvectors are directions that the transformation `C` only stretches; those are the principal components. **Eigenvalues** are the variance along each one.
4. Sort by eigenvalue; **project** the data onto the top `k` eigenvectors: `Z = X W_k`.

Choose `k` by the cumulative **explained-variance ratio** (say 95%). In practice it's computed via SVD. Visualize the transformation intuition with GeoGebra's matrix-transformation tool (linked in the source).

## Notes

- Components are linear and uncorrelated, which removes [[Multicollinearity]] (PCA regression, PLS).
- Linear only; for non-linear structure use kernel PCA, t-SNE or UMAP (visualization), or [[Autoencoders]] (a linear autoencoder trained with MSE recovers the PCA subspace).
