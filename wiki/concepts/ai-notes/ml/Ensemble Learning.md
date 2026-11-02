---
type: concept
title: "Ensemble Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - ensemble
complexity: intermediate
domain: machine-learning
status: developing
address: c-000361
related:
  - "[[Voting Ensembles]]"
  - "[[Stacking]]"
  - "[[Random Forest]]"
  - "[[Gradient Boosting]]"
  - "[[Bias Variance Tradeoff]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Ensemble Learning/Ensemble Learning.md]]"
---

# Ensemble Learning

Combine multiple models so the group beats any member: the **wisdom of crowds** (the audience poll in KBC, aggregated product reviews). From [[ai-notes|AI-Notes]] (CampusX, *Hands-On ML*).

## Four architectures

| Type | Base models | Training | Combine |
|------|-------------|----------|---------|
| [[Voting Ensembles\|Voting]] | Different algorithms, same data | Parallel | Majority or average |
| [[Stacking]] | Different algorithms | Parallel, then a meta-model | Learned weighting |
| **Bagging** (e.g. [[Random Forest]]) | Same algorithm, resampled data | Parallel | Average or vote |
| **Boosting** (e.g. [[Gradient Boosting]]) | Same weak learner | **Sequential**, each fixes previous errors | Weighted sum |

**Cost**: more compute and memory; can be slow with big data and complex base models.

## Getting diverse models

1. Different algorithms. 2. Same algorithm on different data. 3. Both. Diversity matters: errors that are uncorrelated cancel out.

## Bias and variance

- **Bagging** starts from low-bias, high-variance learners (deep trees) and averages away variance.
- **Boosting** starts from high-bias, low-variance learners (stumps, shallow trees) and sequentially reduces bias.

See [[Bias Variance Tradeoff]].

## Resampling schemes

- **Bagging**: rows sampled **with** replacement (bootstrap).
- **Pasting**: rows **without** replacement.
- **Random subspaces**: sample features only (good for high-dimensional data).
- **Random patches**: sample rows and features.
- **Rotation forest**: PCA on random feature subsets, then trees on the rotated data (more diversity).

> [!gap] Stub in source
> The source's `Bagging-Boosting.md` is a heading-only stub; bagging is covered here and in [[Random Forest]].

Deep learning uses the same idea: DLAI notes ensembles give about +2% in competitions ([[Regularization]], [[DLAI Course 4 - Convolutional Neural Networks]]).
