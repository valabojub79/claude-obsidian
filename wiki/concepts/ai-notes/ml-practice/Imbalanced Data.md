---
type: concept
title: "Imbalanced Data"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - data-quality
  - classification
complexity: intermediate
domain: machine-learning
status: developing
address: c-000380
related:
  - "[[Classification Metrics]]"
  - "[[Cross Validation]]"
  - "[[K Nearest Neighbors]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Imbalanced data.md]]"
---

# Imbalanced Data

From [[ai-notes|AI-Notes]] (CampusX; "Stop using SMOTE for everything").

- **Classification**: classes are unevenly represented (fraud, rare disease).
- **Regression**: targets concentrate in a narrow range with a sparse tail (house prices).
- **Causes**: collection or entry errors, or the **natural phenomenon** itself.

## Why it hurts

The model leans toward the majority class, and **accuracy misleads**: with 95 genuine and 5 fraud transactions, "always genuine" scores 95%. See [[Classification Metrics]].

## Remedies

### 1. Resampling (training data only, never the test set)

- **Undersampling** the majority class: fast, but with extreme imbalance it discards most of the data, raising bias.
- **Oversampling** the minority class:
  - **Random oversampling** duplicates rows, which risks overfitting.
  - **SMOTE**: pick a minority point, find its k nearest minority neighbors ([[K Nearest Neighbors]]), and create a synthetic point by **interpolation** `x_new = x + lambda (x_nn - x)`, with `lambda ~ U(0,1)`. Downsides: compute cost, sensitivity to `k`, and unrealistic points in overlapping regions.
  - **ADASYN**: generates more synthetic points for **hard** minority examples (near the boundary or in sparse regions).

(The source has a typo saying oversampling "down samples the majority class"; it **up-samples the minority**.)

### 2. Better metrics

F1, precision and recall per class, the full classification report, PR-AUC.

### 3. Cost-sensitive learning

Weight errors on the minority class more heavily (`class_weight='balanced'`, a custom loss, focal loss).

### 4. Robust models

Boosted trees (XGBoost with `scale_pos_weight`), ensembles of balanced bags.

Always split with **stratified** CV ([[Cross Validation]]) and resample *inside* each training fold to avoid leakage.
