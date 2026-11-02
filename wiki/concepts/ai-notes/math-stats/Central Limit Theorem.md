---
type: concept
title: "Central Limit Theorem"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - probability
complexity: intermediate
domain: mathematics
status: developing
address: c-000342
related:
  - "[[Confidence Interval]]"
  - "[[Z Test]]"
  - "[[Cross Validation]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Central limit theorem.md]]"
---

# Central Limit Theorem (CLT)

From [[ai-notes|AI-Notes]] (CampusX).

## Sampling distribution

Repeatedly draw samples from a population, compute a statistic (say the mean) on each, and plot those values. That's the statistic's **sampling distribution**, and it shows how much the statistic varies.

## The theorem

For independent samples of size `n` from **any** population with finite mean `mu` and variance `sigma^2`, the distribution of the sample mean approaches **normal** as `n` grows:

```
x_bar ~ N(mu, sigma^2 / n)        (n >= 30 is the usual rule of thumb)
```

The **standard error** is `sigma / sqrt(n)`.

## Practical use: estimating a population mean

Average income of working Indian men: you can't survey everyone.

1. Draw many random, reasonably large samples.
2. Compute each sample mean; their distribution is roughly normal.
3. Its center estimates `mu`.
4. Since a point estimate alone isn't trustworthy, use the standard error to build a [[Confidence Interval]].

## In ML: how stable is my model's score?

1. Run k-fold [[Cross Validation]]; average the fold scores.
2. Repeat with different shuffles 30 to 50 times.
3. The distribution of those means is roughly normal (CLT). Its spread shows how variable your model's performance is, and lets you put error bars on reported metrics.

The CLT also justifies [[Z Test|z-tests]] on means and proportions, such as A/B tests ([[AB Testing]]).
