---
type: concept
title: "Probability Distributions"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - probability
  - statistics
complexity: beginner
domain: mathematics
status: developing
address: c-000352
related:
  - "[[Bernoulli Distribution]]"
  - "[[Uniform Distribution]]"
  - "[[Log Normal Distribution]]"
  - "[[Pareto Distribution]]"
  - "[[Central Limit Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Probability Distributions.md]]"
---

# Probability Distributions

Hub page for [[ai-notes|AI-Notes]]' probability section. A distribution assigns probabilities to a random variable's outcomes: a **PMF** for discrete variables, a **PDF** for continuous ones, and a **CDF** `P(X <= x)` for both.

| Distribution | Type | Parameters | Mean / Variance | Typical data | Page |
|-------------|------|-----------|-----------------|--------------|------|
| Bernoulli | Discrete | `p` | `p` / `p(1-p)` | One yes/no trial | [[Bernoulli Distribution]] |
| Binomial | Discrete | `n, p` | `np` / `np(1-p)` | Successes in `n` trials | (source empty) |
| Uniform | Both | `a, b` | `(a+b)/2` / `(b-a)^2/12` | Random init, dice | [[Uniform Distribution]] |
| Normal | Continuous | `mu, sigma` | `mu` / `sigma^2` | Heights, measurement errors, sample means ([[Central Limit Theorem]]) | (source empty; see [[Measures of Central Tendency]]) |
| Log-normal | Continuous | `mu, sigma` (of `ln X`) | `exp(mu + sigma^2/2)` / `(exp(sigma^2) - 1) exp(2mu + sigma^2)` | Incomes, time on page | [[Log Normal Distribution]] |
| Pareto | Continuous | `x_m, alpha` | `alpha x_m/(alpha - 1)` for alpha > 1 | Wealth, city sizes (power law) | [[Pareto Distribution]] |
| Student's t | Continuous | `df` | 0 / `df/(df-2)` | Small-sample means | [[T Test]] |

Why ML cares: choosing losses (Gaussian noise leads to MSE, Bernoulli to cross-entropy; see [[Logistic Regression]]), [[Naive Bayes]] likelihoods, initialization ([[Weight Initialization]]), transformations toward normality ([[Transformations]]), and hypothesis tests ([[Hypothesis Testing]]).
