---
type: concept
title: "Uniform Distribution"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - probability
complexity: beginner
domain: mathematics
status: developing
address: c-000356
related:
  - "[[Probability Distributions]]"
  - "[[Weight Initialization]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Uniform Distribution.md]]"
---

# Uniform Distribution

Every outcome in a range is **equally likely**. From [[ai-notes|AI-Notes]].

- **Discrete**: a fair die, `P = 1/6` each.
- **Continuous** on `[a, b]`:

```
f(x) = 1 / (b - a)  for a <= x <= b, else 0
F(x) = (x - a) / (b - a)   =>  P(X < c) = (c - a)/(b - a)
E[X] = (a + b)/2,   Var[X] = (b - a)^2 / 12,   skewness = 0
```

- Parameters: `a`, `b` (lower and upper bound). MLE from data: `a_hat = min(x)`, `b_hat = max(x)`.
- **Examples** (from the source): the height of a random person from a group spanning 5'0" to 6'0", or an apple between 100 and 200 g, treated as uniform. Realistic data is usually closer to normal; uniform is a modeling simplification.

## In ML and deep learning

- **Weight initialization**: `U(-r, r)` (Glorot uniform; see [[Weight Initialization]]).
- **Random search** over hyperparameters (on a log scale for learning rates; see [[Hyperparameter Tuning]]).
- **Data augmentation**: random brightness, contrast or rotation factors drawn uniformly ([[Data Augmentation]]).
- Monte Carlo simulation: uniform samples transformed into other distributions (inverse-CDF sampling).
- **Maximum entropy** among distributions on a bounded interval: `log(b - a)`.

> [!gap] Many questions unanswered in source
> PDF/CDF derivations, goodness-of-fit testing and Monte Carlo details are listed as questions without answers; the standard answers are filled in above.
