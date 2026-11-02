---
type: concept
title: "Bernoulli Distribution"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - probability
complexity: beginner
domain: mathematics
status: developing
address: c-000341
related:
  - "[[Probability Distributions]]"
  - "[[Naive Bayes]]"
  - "[[Chi Square Test]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/Bernoulli Distribution.md]]"
---

# Bernoulli Distribution

A discrete distribution for a **single binary trial** (success 1, failure 0). From [[ai-notes|AI-Notes]].

```
P(X = x) = p^x (1 - p)^(1 - x),   x in {0, 1}
E[X] = p,   Var[X] = p(1 - p)
```

- One parameter `p`: P(success). A fair coin has `p = 0.5`; a biased coin has some other `p`.
- Examples: one coin toss; one die roll classified as even or not.
- **Not appropriate** with more than 2 outcomes (use categorical or multinomial) or continuous outcomes.
- **Check fit**: are there exactly two outcomes? Then a [[Chi Square Test|chi-square]] goodness-of-fit test.
- **Estimate `p`** by [[Maximum Likelihood Estimation|MLE]]: `p_hat = (number of successes) / n`, the sample mean.

In ML: binary labels (logistic regression's likelihood, giving binary cross-entropy), Bernoulli [[Naive Bayes]], and dropout masks ([[Dropout]]). A sum of `n` independent Bernoullis is **Binomial(n, p)**.
