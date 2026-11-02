---
type: concept
title: "Hypothesis Testing"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - hypothesis-testing
complexity: intermediate
domain: mathematics
status: developing
address: c-000346
related:
  - "[[Z Test]]"
  - "[[T Test]]"
  - "[[Chi Square Test]]"
  - "[[ANOVA Test]]"
  - "[[AB Testing]]"
  - "[[Confidence Interval]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Hypothesis Testing.md]]"
---

# Hypothesis Testing

Test an assumption about an unknown **population parameter** using a sample. From [[ai-notes|AI-Notes]] (CampusX, Professor Leonard).

- **Null hypothesis H0**: the default, assumed true until the evidence says otherwise (no effect or difference).
- **Alternative H1 / Ha**: contradicts H0.
- **Failing to reject H0 doesn't prove it true**; it means insufficient evidence for H1, since we only ever see a sample.

## Key terms

| Term | Meaning |
|------|---------|
| **Significance level alpha** | P(reject H0 when H0 is true), the **Type I** error rate (often 0.05) |
| **Confidence level** | `1 - alpha` |
| **Beta / power** | Beta = P(fail to reject a false H0), the **Type II** error rate; power = `1 - beta` |
| **Critical (rejection) region** | Test-statistic values that lead to rejecting H0, set by alpha and the tail direction |
| **p-value** | P(data at least this extreme given H0). Small p means the sample is surprising under H0 |

> [!contradiction] Confidence level
> The source defines confidence level as "the probability of accepting H0 even though it is wrong". That is **beta** (Type II error). Confidence level is `1 - alpha`, the probability of *not* rejecting a *true* H0.

## Two decision approaches

1. **Rejection region**: reject if the statistic falls in the critical region. It gives a yes/no answer only, no strength of evidence.
2. **p-value**: reject if `p < alpha`. It also conveys strength.

## Choosing a test

| Situation | Test |
|-----------|------|
| Mean, sigma known, large n | [[Z Test]] |
| Mean, sigma unknown | [[T Test]] |
| Categorical fit or independence | [[Chi Square Test]] |
| 3+ group means | [[ANOVA Test]] |
| Regression overall significance | F-test ([[Regression Analysis]]) |
| Product experiments | [[AB Testing]] |

Related: [[Confidence Interval]] (the estimation counterpart), [[Central Limit Theorem]].
