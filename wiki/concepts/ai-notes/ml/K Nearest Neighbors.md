---
type: concept
title: "K Nearest Neighbors"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - classification
  - regression
  - instance-based
complexity: beginner
domain: machine-learning
status: developing
address: c-000363
related:
  - "[[Feature Scaling]]"
  - "[[Missing Values]]"
  - "[[Principal Component Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Instance Based Models/K Nearest Neighbor.md]]"
---

# K Nearest Neighbors (KNN)

Distance-based supervised learning for classification (**majority vote** of the K nearest points) and regression (**mean**, or distance-weighted mean, of their targets). From [[ai-notes|AI-Notes]].

- **Lazy learner**: "training" just stores the data; all work happens at prediction time.
- **Non-parametric**: no assumed form; effectively the whole training set is the model.

## Choosing K

- Rule of thumb: `K` about `sqrt(N)`; then tune with [[Cross Validation]].
- Use **odd K** for binary classification to avoid ties.
- Small K: overfits (low bias, high variance; listens to noise). Large K: underfits (high bias, low variance).

## Hyperparameters

`n_neighbors`; distance metric (**Euclidean**, **Manhattan** (taxicab), **Minkowski** `(sum |x-y|^p)^(1/p)`, which generalizes both: p=1 Manhattan, p=2 Euclidean); `weights` (uniform or inverse-distance); search algorithm (brute force, **KD-tree**, **Ball tree**).

## Speed-ups

- **KD-tree**: recursively split space with axis-aligned hyperplanes at feature medians.
- **Ball tree**: nested hyperspheres; better in higher dimensions.
- Both cut query cost from `O(N)` toward `O(log N)` in low dimensions.

## Must-dos

- **Scale features**: distances are unit-dependent ([[Feature Scaling]]).
- Remove [[Outliers]]; reduce dimensions ([[Principal Component Analysis]]).

## Curse of dimensionality

In high dimensions all points become nearly equidistant (the nearest-to-farthest distance ratio approaches 1), so "nearest" stops meaning anything, and compute grows too.

## Uses

Anomaly detection, recommenders (similar users or items), **KNN imputation** of missing values ([[Missing Values]]).
