---
type: concept
title: "Random Forest"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - trees
  - ensemble
complexity: intermediate
domain: machine-learning
status: developing
address: c-000368
related:
  - "[[Decision Tree]]"
  - "[[Ensemble Learning]]"
  - "[[Gradient Boosting]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Tree Based Models/Random Forest.md]]"
---

# Random Forest

**Bagging** of [[Decision Tree|decision trees]] plus **random feature subsets at each split**, which decorrelates the trees. From [[ai-notes|AI-Notes]] (CampusX sessions).

## Bagging vs random forest

| | Bagging | Random forest |
|-|---------|---------------|
| Base model | Any (all of one type) | Decision trees only |
| Row sampling | Per tree (bootstrap) | Per tree (bootstrap) |
| Column sampling | Optional, per tree | **Per node** (default `sqrt(F)` features for classification) |

## Why a forest beats one tree

A single fully grown tree has low bias and **high variance**: a small change in the data gives a very different tree. Averaging many decorrelated trees keeps the low bias and **cuts variance**. Individual outliers or noise affect only some trees, so the forest is robust.

## Out-of-bag (OOB) evaluation

Each bootstrap sample omits about **37%** of rows (`(1 - 1/N)^N` is about `1/e`). For every row, predict using only the trees that didn't see it and aggregate. The result is the **OOB score**, a free validation estimate. `OOB error = 1 - OOB score`. (The source describes it as averaging per-tree accuracies; the standard computation aggregates per-sample votes across the trees for which that sample was out of bag.)

## Feature importance

The average of the trees' impurity-based importances (or permutation importance, which is less biased toward high-cardinality features).

## Key hyperparameters (scikit-learn)

`n_estimators` (more is better but slower), `max_features`, `max_depth`, `min_samples_split`, `min_samples_leaf`, `max_leaf_nodes`, `min_impurity_decrease`, `bootstrap`, `max_samples`, `oob_score`, `class_weight` (imbalance; see [[Imbalanced Data]]), `ccp_alpha` (pruning), `n_jobs`, `warm_start`, `random_state`.

## Extra Trees (extremely randomized trees)

For each candidate feature, draw a **random** threshold (instead of searching for the optimal one), then pick the best among those random splits. Even more decorrelation, and faster to train. Sometimes better, sometimes worse; validate.
