---
type: concept
title: "AB Testing"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - experimentation
complexity: intermediate
domain: mathematics
status: developing
address: c-000339
related:
  - "[[Hypothesis Testing]]"
  - "[[Z Test]]"
  - "[[T Test]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/AB Testing.md]]"
---

# A/B Testing

**Split testing**: compare two versions of something on randomized groups to decide, with data, which is better. Widely used in marketing and product work. From [[ai-notes|AI-Notes]] (freeCodeCamp, PW Skills, CodeBasics).

- **Control group (A)**: unchanged, the reference.
- **Treatment / experimental group (B)**: exposed to the change.

## Worked example: green vs blue "Buy" button

1. **Objective**: do purchases increase?
2. **Hypotheses**: H0, the green button doesn't change the conversion rate; H1, it does (see [[Hypothesis Testing]]).
3. **Randomize**: 50% of visitors see blue (A), 50% see green (B).
4. **Measure**: purchases per group for about a month.
5. **Analyze**: compare conversion **proportions** with a **two-proportion [[Z Test]]**; continuous metrics (revenue per user) with a two-sample [[T Test]].
6. **Decide**: if `p < alpha`, reject H0.

## Pitfalls

- **Sampling bias**: groups must be randomly assigned.
- **Sample size**: too small gives noisy, flip-flopping results. Compute the required `n` up front (power analysis) and don't stop early when results look good ("peeking" inflates false positives).
- Novelty effects, seasonality, multiple metrics (multiple comparisons).

## In machine learning

- **Model comparison in production**: route users randomly to recommender A or B; compare click-through or conversion (proportion z-test) or engagement time (t-test).
- **Feature impact**: model with vs without a new feature, evaluated on the same validation data (paired t-test).

More than two variants (A/B/C/D, multivariate) is possible but needs corrections for multiple comparisons (or [[ANOVA Test|ANOVA]] for means), or bandit algorithms.
