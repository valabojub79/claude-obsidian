---
type: concept
title: "ANOVA Test"
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
address: c-000340
related:
  - "[[Hypothesis Testing]]"
  - "[[T Test]]"
  - "[[Feature Selection]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/ANOVA test.md]]"
---

# ANOVA (Analysis of Variance)

Tests whether **3 or more group means** differ, using the **F-distribution**: the ratio of two chi-square variables, each divided by its degrees of freedom. From [[ai-notes|AI-Notes]].

- **One-way ANOVA**: one categorical factor, continuous outcome.
- **Two-way ANOVA**: two factors (main effects plus their **interaction**).

## The F statistic

```
SSB = sum_groups n_g (mean_g - grand_mean)^2     df_B = k - 1
SSW = sum_groups sum_i (x_i - mean_g)^2          df_W = n - k
F = (SSB / df_B) / (SSW / df_W)                  # between-group variance / within-group variance
```

A large F means the group means differ more than within-group noise would explain.

## Example

A school tests 3 teaching methods. H0: all three mean scores are equal. Compute F, get the p-value from `F(k-1, n-k)`; if `p < alpha`, at least one mean differs. Follow up with post-hoc tests (Tukey HSD) to find which.

Assumptions: independence, roughly normal residuals, equal variances (Levene's test; use Welch's ANOVA if they're unequal).

## In ML: feature selection

One-way ANOVA F-test between a **numeric feature** and a **categorical target** (`f_classif` in scikit-learn). Features whose means differ strongly across classes are informative. See [[Feature Selection]]. With exactly 2 groups, ANOVA is equivalent to a t-test (`F = t^2`; see [[T Test]]).
