---
type: concept
title: "T Test"
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
address: c-000354
related:
  - "[[Z Test]]"
  - "[[Hypothesis Testing]]"
  - "[[ANOVA Test]]"
  - "[[Feature Selection]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Probability/T test.md]]"
---

# T-Test

A hypothesis test based on **Student's t-distribution**, used when the **population standard deviation is unknown** and estimated from the sample. From [[ai-notes|AI-Notes]].

> [!contradiction] Sample-size condition
> The source lists "at least 30 samples" as a condition. The t-test is designed precisely for **small samples** with unknown `sigma`; it works for any `n` if the data are roughly normal. For large `n` the t- and z-tests agree.

## The t-distribution

Bell-shaped like the normal but with **heavier tails**, controlled by **degrees of freedom** (`df = n - 1` for one sample). Low df means heavier tails (more uncertainty in `s`); as df grows it approaches N(0, 1).

## Variants

```
one-sample:      t = (x_bar - mu_0) / (s / sqrt(n)),                   df = n - 1
two-sample:      t = (x1_bar - x2_bar) / sqrt(s1^2/n1 + s2^2/n2)       (Welch; df via Welch-Satterthwaite)
pooled (equal variances): df = n1 + n2 - 2
paired:          one-sample t on the differences
```

## In machine learning

1. **Model comparison**: compare per-fold scores of two models across the same CV folds with a **paired** t-test. (Caveat: CV folds overlap, so use corrected tests such as the Nadeau-Bengio corrected resampled t-test.)
2. **Feature selection** for binary classification: does a numeric feature's mean differ between the classes? (Use [[ANOVA Test|ANOVA]] for more than 2 classes; see [[Feature Selection]].)

Steps as in [[Hypothesis Testing]]; compare [[Z Test]].
