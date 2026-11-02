---
type: concept
title: "Z Test"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - hypothesis-testing
complexity: beginner
domain: mathematics
status: developing
address: c-000357
related:
  - "[[Hypothesis Testing]]"
  - "[[T Test]]"
  - "[[Central Limit Theorem]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Z test.md]]"
---

# Z-Test

A hypothesis test using the **standard normal (Z) distribution**. From [[ai-notes|AI-Notes]].

**Use when**: comparing a sample mean to a hypothesized mean, or two group means, with:

1. Large sample (`n >= 30`), so the [[Central Limit Theorem]] makes the sample mean roughly normal;
2. **Known population standard deviation** `sigma`;
3. Data from a (roughly) normal population, or large `n`.

```
z = (x_bar - mu_0) / (sigma / sqrt(n))                                  # one-sample
z = (x1_bar - x2_bar) / sqrt(sigma1^2/n1 + sigma2^2/n2)                 # two-sample
```

## Steps

1. State H0 and H1.
2. Compute `z`.
3. Get the p-value from N(0, 1) (one or two-tailed).
4. Compare to the significance level alpha (say 0.05): if `p < alpha`, reject H0.

Also used for **proportions** (A/B conversion rates; see [[AB Testing]]). If `sigma` is unknown, use the [[T Test]]. Framework: [[Hypothesis Testing]].
