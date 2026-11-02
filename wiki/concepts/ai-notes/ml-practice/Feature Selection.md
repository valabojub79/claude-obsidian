---
type: concept
title: "Feature Selection"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - feature-engineering
complexity: intermediate
domain: machine-learning
status: developing
address: c-000378
related:
  - "[[Lasso Regression]]"
  - "[[Decision Tree]]"
  - "[[Chi Square Test]]"
  - "[[ANOVA Test]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Feature Selection.md]]"
---

# Feature Selection

Choose a subset of the most useful features to cut model complexity, speed up training, reduce overfitting, and aid analysis. Unlike **feature extraction**, which *creates* new features (PCA, embeddings), selection keeps a subset of the originals. From [[ai-notes|AI-Notes]] (CampusX sessions 54 to 56).

## 1. Filter methods (statistics, model-free)

Score each feature, keep those above a threshold:

- Remove **duplicate** features.
- **Variance threshold**: drop constant and quasi-constant features.
- **Correlation** with the target (and drop highly inter-correlated features; see [[Multicollinearity]]).
- **[[ANOVA Test|ANOVA]]** F-test (numeric feature, categorical target).
- **[[Chi Square Test|Chi-square]]** test of independence (categorical feature and target).
- **Mutual information** (captures non-linear dependence).

Fast, but **univariate**: they miss interactions (a feature useless alone may be strong combined with others).

## 2. Wrapper methods (search with a model)

Score feature **subsets** by model performance:

- **Exhaustive** (best-subset): all `2^n` combinations, which is prohibitive.
- **Forward selection**: start empty and add the best feature each round.
- **Backward elimination**: start full and drop the least useful each round.
- **Recursive feature elimination (RFE)**: fit, drop the weakest by importance or coefficient, refit, repeat.

More accurate, but expensive and prone to overfitting the selection.

## 3. Embedded methods (selection during training)

- **[[Lasso Regression]]**: L1 drives coefficients to 0.
- **Tree importances** ([[Decision Tree]], [[Random Forest]], [[Gradient Boosting]]).
- Linear model coefficients (on scaled features).

A good compromise between cost and accuracy.
