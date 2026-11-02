---
type: concept
title: "Hyperparameter Tuning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000161
related:
  - "[[Parameters vs Hyperparameters]]"
  - "[[Optimization Algorithms]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Hyperparameter Tuning

## Priority (Ng's rough ordering)

1. Learning rate `alpha` (most important).
2. Momentum `beta`, mini-batch size, number of hidden units.
3. Number of layers, learning-rate decay.
4. Adam's `beta1`, `beta2`, `eps` (almost never tuned).

Regularization `lambda` and activation choice also matter; it depends on the problem.

## Search strategy

- **Random search, not grid.** Each trial explores a new value of every hyperparameter, so you learn more about the ones that matter.
- **Coarse to fine:** find a good region, then sample densely inside it.

## Sample on the right scale

For `alpha` in `[1e-4, 1]`, sample the exponent uniformly:

```python
r = -4 * np.random.rand()     # r in [-4, 0]
alpha = 10 ** r
```

For momentum `beta` in `[0.9, 0.999]`, sample `1 - beta` on a log scale in `[1e-3, 1e-1]`. The output is very sensitive to `beta` near 1.

## Pandas vs caviar

- **Panda:** compute-poor. Babysit one model, nudging hyperparameters day by day.
- **Caviar:** compute-rich. Train many models in parallel and pick the best.

Re-evaluate every few months: intuitions decay as data and hardware change, and settings don't always transfer between domains.

## Related

[[ai-notes|AI-Notes]] covers grid, random and Bayesian search from the ML side: [[Hyperparameter Optimization]].
