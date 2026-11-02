---
type: concept
title: "Naive Bayes"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - classification
  - probabilistic
complexity: intermediate
domain: machine-learning
status: developing
address: c-000366
related:
  - "[[Bernoulli Distribution]]"
  - "[[Probability Distributions]]"
  - "[[Text Preprocessing]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Bayesian Models/Naive Bayes.md]]"
---

# Naive Bayes

A probabilistic classifier built on **Bayes' theorem** with the **naive** assumption that features are conditionally independent given the class. From [[ai-notes|AI-Notes]] (CampusX).

```
P(A|B) = P(B|A) P(A) / P(B)                               # Bayes' theorem
P(y | x1..xn) proportional to P(y) * prod_i P(x_i | y)    # Naive Bayes
y_hat = argmax_y P(y) prod_i P(x_i | y)
```

Conditional probability is `P(A|B)` itself; Bayes' theorem **relates** `P(A|B)` to `P(B|A)`.

- **Training** = estimating priors `P(y)` and per-feature likelihoods `P(x_i|y)` (the model parameters). Fast, and works with small data.
- Parametric (it assumes independence and a distributional form).

## Why "naive"?

1. **Tractability**: the full joint `P(x1..xn | y)` needs about `k^n` probabilities; independence needs about `n*k`.
2. **Variance control**: the full joint would be extremely specific (low bias, high variance); the assumption regularizes.

## Numerical issues

- **Underflow**: products of many small probabilities, so sum **log-probabilities** and pick the largest (least negative).
- **Zero probabilities** (feature value unseen with a class): **Laplace / additive smoothing** `P(x|y) = (count + alpha) / (N_y + alpha * K)`, where `K` is the number of possible feature values.
- **alpha's bias-variance**: large alpha pushes likelihoods toward uniform (0.5 for binary features), so priors dominate and the model underfits; tiny alpha is sensitive to sparse counts and overfits.

## Variants

| Variant | Features | Typical use |
|---------|----------|-------------|
| **Gaussian NB** | Continuous, roughly normal (transform if not; see [[Transformations]]) | Tabular numeric. No smoothing needed: densities are never exactly 0 |
| **Bernoulli NB** | Binary | Word presence |
| **Categorical NB** | Multi-category | Color, shape |
| **Multinomial NB** | Counts | **Text** (word frequencies) |
| Complement NB | Counts | Imbalanced text (source stub) |

**Out-of-core** NB: `partial_fit` on batches when data doesn't fit in memory.

Example (Gaussian): P(placed | CGPA=3.6, IQ=100) is proportional to P(placed) * N(3.6; mu, sigma for placed CGPA) * N(100; mu, sigma for placed IQ).
