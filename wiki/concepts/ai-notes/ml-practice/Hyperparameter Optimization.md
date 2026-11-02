---
type: concept
title: "Hyperparameter Optimization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - model-tuning
complexity: intermediate
domain: machine-learning
status: developing
address: c-000379
related:
  - "[[Hyperparameter Tuning]]"
  - "[[Cross Validation]]"
  - "[[Parameters vs Hyperparameters]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Hyperparameter Optimization.md]]"
---

# Hyperparameter Optimization

From [[ai-notes|AI-Notes]]. The deep-learning-specific view (log-scale sampling, pandas vs caviar) is [[Hyperparameter Tuning]].

- **Parameters** are learned (regression coefficients, NN weights). **Hyperparameters** steer learning (K in KNN, `max_depth`, learning rate). See [[Parameters vs Hyperparameters]].

## Search strategies

| Method | Idea | Trade-off |
|--------|------|-----------|
| **Grid search CV** | Every combination on a grid, each with k-fold CV | 2 params x 5 values x 5 folds = **125 fits**; explodes combinatorially |
| **Randomized search CV** | Sample `n_iter` random combinations | Far cheaper; may miss the optimum (but usually finds near-optimal; see DLAI) |
| **Bayesian optimization** | A surrogate model of score vs hyperparameters picks promising next points | Fewer evaluations; libraries **Optuna**, **Hyperopt**, Keras Tuner |

**Tune on validation (CV) folds, never the test set**: optimizing against test data leaks information and gives optimistic estimates ([[Cross Validation]]).

## Neural-network knobs that matter most (per the notes)

Number of hidden layers, neurons per layer, learning rate, optimizer, batch size, activation functions, epochs (use early stopping).

- Prefer **more layers with fewer neurons** over one huge layer: **representation learning** builds features hierarchically (edges, then shapes, then objects), and lower layers transfer to related tasks (human-face to monkey-face detector). See [[Transfer Learning]].
- Keep adding layers until overfitting appears, then regularize.
