---
type: concept
title: "Missing Values"
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
address: c-000381
related:
  - "[[Outliers]]"
  - "[[K Nearest Neighbors]]"
  - "[[Random Forest]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Missing Values.md]]"
---

# Missing Values

From [[ai-notes|AI-Notes]]. Shown as `NaN` in pandas.

**Causes**: data-entry errors, faulty instruments, careless preprocessing (a transform applied outside its domain, such as `log` of a value at or below 0), and data-management problems when merging sources into a warehouse.

**Harm**: most algorithms can't accept `NaN`; and missing data reduces statistical power and can bias inferences about the population.

## Missingness mechanisms

| Type | Meaning | Typical handling |
|------|---------|------------------|
| **MCAR** (completely at random) | Unrelated to any data | Deletion or univariate imputation is unbiased |
| **MAR** (at random) | Depends on *observed* features | Multivariate imputation |
| **MNAR** (not at random) | Depends on the missing value itself, or was deliberate | Multivariate imputation plus a missing-indicator feature; model the mechanism |

## Strategies

- **Complete case analysis (CCA)**: drop rows with missing values. Only when the column has under about 5% missing and the data is MCAR. In production, rows with missing fields can't be scored, so you need an imputation path anyway.
- **Univariate imputation** (mean, median, mode, constant, arbitrary value, end-of-distribution): fine for small amounts of missingness.
- **Multivariate imputation** (larger amounts):
  - **KNN imputer** ([[K Nearest Neighbors]]).
  - **MICE** (iterative chained equations with linear or logistic models; multiple imputed datasets).
  - **MissForest** (iterative [[Random Forest]] imputation; captures non-linear relationships).
- Add a **missing indicator** column when missingness itself may be informative.

## Detecting

`df.isnull().sum()` / `isna()`; the `missingno` matrix and bar plots, whose patterns hint that data is *not* MCAR.

Fit imputers on the training set only, then transform validation and test.
