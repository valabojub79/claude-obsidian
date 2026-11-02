---
type: concept
title: "Gradient Checking"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - debugging
complexity: intermediate
domain: deep-learning
status: developing
address: c-000158
related:
  - "[[Backpropagation]]"
  - "[[Dropout]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Gradient Checking

Verify a hand-written [[Backpropagation]] by comparing it against a numerical estimate.

## Two-sided difference

```
dtheta_approx[i] = ( J(theta + eps*e_i) - J(theta - eps*e_i) ) / (2*eps)
```

The two-sided form has error `O(eps^2)`, versus `O(eps)` for the one-sided form. Use `eps` around `1e-7`.

## Procedure

1. Reshape all `W[l], b[l]` into one vector `theta`, and all `dW[l], db[l]` into `dtheta`.
2. Compute `dtheta_approx` for every component.
3. Compare: `diff = ||dtheta_approx - dtheta|| / (||dtheta_approx|| + ||dtheta||)`

| diff | Verdict |
|------|---------|
| < 1e-7 | Great |
| ~1e-5 | Inspect for suspicious components |
| > 1e-3 | Very likely a bug |

## Rules

- Debugging only: it's far too slow to run while training.
- If it fails, find which components (which `dW[l]` or `db[l]`) disagree.
- Include the regularization term in `J`.
- Doesn't work with [[Dropout]]: set `keep_prob = 1` while checking.
- Run at random init and again after some training: some bugs only show once weights grow.
