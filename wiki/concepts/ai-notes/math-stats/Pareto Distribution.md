---
type: concept
title: "Pareto Distribution"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - probability
  - power-law
complexity: intermediate
domain: mathematics
status: developing
address: c-000351
related:
  - "[[Probability Distributions]]"
  - "[[Log Normal Distribution]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Pareto Distribution.md]]"
---

# Pareto Distribution

A continuous **power-law** distribution: a few items hold most of the mass (the "80/20 rule"). Power law: `y = k * x^(-alpha)`. From [[ai-notes|AI-Notes]].

```
f(x) = alpha * x_m^alpha / x^(alpha + 1),   x >= x_m
P(X > x) = (x_m / x)^alpha
mean = alpha x_m / (alpha - 1)   (alpha > 1;  infinite otherwise)
```

## Shape parameter alpha

- **Small alpha**: **heavy tail**, extreme values common, more inequality (mean or variance may be infinite).
- **Large alpha**: **light tail**, mass concentrated near `x_m`.

> [!contradiction] Direction of the alpha effect
> The source says that high alpha *increases* skewness. For the Pareto distribution, skewness **decreases** as alpha grows (it is finite only for alpha > 3, and falls toward 2 as alpha goes to infinity). Larger alpha means lighter tails and less skew.

## Examples

Wealth distribution (Pareto's original observation: a small share of people own most wealth), city populations, word frequencies (Zipf), file sizes, website traffic.

## Detecting it

- **Log-log plot** of the survival function (or rank vs size) is roughly a **straight line** with slope `-alpha`.
- **Q-Q plot** against a fitted Pareto.

Distinguishing it from [[Log Normal Distribution|log-normal]] tails is notoriously hard with limited data.
