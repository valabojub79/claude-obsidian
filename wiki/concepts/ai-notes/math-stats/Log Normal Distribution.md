---
type: concept
title: "Log Normal Distribution"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - probability
complexity: beginner
domain: mathematics
status: developing
address: c-000347
related:
  - "[[Probability Distributions]]"
  - "[[Transformations]]"
  - "[[Outliers]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Log Normal Distribution.md]]"
---

# Log-Normal Distribution

`X` is log-normal if `ln X` is **normally** distributed. Continuous, positive, **right-skewed** with a long tail. From [[ai-notes|AI-Notes]].

```
f(x) = 1 / (x sigma sqrt(2 pi)) * exp( -(ln x - mu)^2 / (2 sigma^2) ),   x > 0
E[X] = exp(mu + sigma^2/2)
Var[X] = (exp(sigma^2) - 1) * exp(2 mu + sigma^2)
```

Here `mu` and `sigma` are the mean and standard deviation of `ln X`, not of `X`.

- Changing `mu` mostly **shifts and scales**; changing `sigma` changes the **shape and spread** (larger sigma means heavier skew).
- Arises from **multiplicative** processes (products of many positive factors), just as normals arise from sums.
- **Data-science examples**: comment lengths on social media, minutes spent on articles, incomes.

**Practical tip**: a `log` transform turns it into a normal distribution, which helps linear models and tests that assume normality ([[Transformations]]) and tames [[Outliers]].
