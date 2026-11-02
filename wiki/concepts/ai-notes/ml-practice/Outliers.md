---
type: concept
title: "Outliers"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - data-quality
  - preprocessing
complexity: beginner
domain: machine-learning
status: developing
address: c-000383
related:
  - "[[Missing Values]]"
  - "[[Feature Scaling]]"
  - "[[Measures of Central Tendency]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Outliers.md]]"
---

# Outliers

Points that deviate **significantly** from the rest. From [[ai-notes|AI-Notes]].

**Causes**: data-entry errors (1,000,000 instead of 100,000), measurement faults, careless transformations, or genuine rare events.

**Outlier vs noise**: heights mostly 160 to 170 cm, so 172 to 175 cm is *noise* (small deviation) while 150 or 200 cm is an *outlier* (extreme).

## Why they matter

- They distort distance-based models (KNN) and least squares (linear regression); **trees are robust**.
- They inflate MSE and RMSE ([[Regression Metrics]]) and skew LOOCV ([[Cross Validation]]).
- **But they can be signal**: in the author's Udemy-pricing project, a cluster of courses with very high subscriber counts was a real segment worth modeling, not an error. Investigate before deleting.

## Types

- **Global**: extreme relative to everything (a 7-foot person).
- **Contextual**: extreme only in context (35°C in winter).
- **Collective**: a group that's anomalous together (a sudden traffic spike, a possible attack).

## Detection

- **Roughly normal feature**: the [[Empirical Rule|empirical rule]] or z-score (beyond +/-3 sigma).
- **Skewed feature**: **IQR fences** `[Q1 - 1.5*IQR, Q3 + 1.5*IQR]` (see [[Measures of Dispersion]]).
- Plots: box plot, scatter plot, histogram. Multivariate: isolation forest, LOF, DBSCAN noise points ([[Clustering Algorithms]]).

## Treatment

1. **Trimming**: remove (risks data loss).
2. **Capping (winsorization)**: clip to percentile or IQR limits.
3. **Binning (discretization)**: outliers fall into the end bins.
4. **Treat as missing**, then impute ([[Missing Values]]).
5. **Transformations**: log, Box-Cox, Yeo-Johnson (see [[Transformations]]).

Or use robust methods: median, MAE or Huber loss, `RobustScaler` ([[Feature Scaling]]).
