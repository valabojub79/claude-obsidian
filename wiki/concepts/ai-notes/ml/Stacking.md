---
type: concept
title: "Stacking"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - ensemble
complexity: intermediate
domain: machine-learning
status: developing
address: c-000371
related:
  - "[[Ensemble Learning]]"
  - "[[Voting Ensembles]]"
  - "[[Cross Validation]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Ensemble Learning/Stacking.md]]"
---

# Stacking

Like [[Voting Ensembles|voting]] (different base models, same data), but a **meta-model** learns how to combine the base predictions, effectively weighting each base model by how reliable it is. From [[ai-notes|AI-Notes]].

- **Train**: fit the base models; generate their predictions; train the meta-model on those predictions to predict the target.
- **Predict**: the query goes through all base models, and the meta-model combines their outputs.

**Leakage warning**: the meta-model must be trained on **out-of-fold** predictions (k-fold [[Cross Validation]]) or a hold-out "blending" set. If the base models predict on data they were trained on, the meta-model learns to over-trust overfit models.

Works for classification (class probabilities in, often logistic regression as the meta-model) and regression (ridge as the meta-model). scikit-learn: `StackingClassifier` and `StackingRegressor`.
