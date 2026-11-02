---
type: concept
title: "Maximum Likelihood Estimation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - probability
complexity: intermediate
domain: mathematics
status: seed
address: c-000348
related:
  - "[[Logistic Regression]]"
  - "[[Bernoulli Distribution]]"
  - "[[Naive Bayes]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Linear Algebra/Maximum Likelihood Estimation.md]]"
---

# Maximum Likelihood Estimation (MLE)

Choose parameters `theta` that make the observed data most probable:

```
theta_hat = argmax_theta  prod_i p(x_i | theta)  =  argmax_theta  sum_i log p(x_i | theta)
```

Logs turn products into sums, which avoids underflow (the same trick as in [[Naive Bayes]]).

Where it shows up in this wiki:

- [[Logistic Regression]]: MLE with Bernoulli outputs gives **binary cross-entropy**.
- [[Linear Regression]]: MLE with Gaussian noise gives **MSE**.
- [[Bernoulli Distribution]]: `p_hat` = the sample proportion of successes.
- Neural-network training minimizes negative log-likelihood ([[LISA Tutorial - Getting Started]]).

> [!gap] Source stub
> The AI-Notes MLE page is empty; this page collects the uses referenced elsewhere.
