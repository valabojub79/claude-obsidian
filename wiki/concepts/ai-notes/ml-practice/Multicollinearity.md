---
type: concept
title: "Multicollinearity"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - regression
  - data-quality
complexity: intermediate
domain: machine-learning
status: developing
address: c-000382
related:
  - "[[Linear Regression]]"
  - "[[Ridge Regression]]"
  - "[[Categorical Encoding]]"
  - "[[Principal Component Analysis]]"
sources:
  - "[[.raw/repos/AI-Notes/General ML Topics/Multicollinearity.md]]"
---

# Multicollinearity

Independent features that are **highly correlated** with each other (CGPA and IQ). **Predictions are mostly unaffected; inference is not**: coefficients become unstable and their standard errors inflate. From [[ai-notes|AI-Notes]].

## Perfect multicollinearity

One feature is an exact linear function of others (percentage = 10 x CGPA; or one-hot encoding without dropping a column, the **dummy-variable trap**; see [[Categorical Encoding]]). Then `X^T X` is **singular** (determinant 0), so the OLS inverse doesn't exist and coefficients can't be computed ([[Linear Regression]]).

## Near-perfect

The determinant is tiny, its reciprocal huge, so the coefficients and their **standard errors** blow up. Small data changes swing coefficients wildly, even flipping signs, so p-values and interpretations become unreliable.

## Detection

1. Correlation matrix (pairwise only).
2. Determinant of `X^T X` near 0.
3. **VIF** (variance inflation factor): `VIF_i = 1 / (1 - R_i^2)`, where `R_i^2` comes from regressing feature `i` on all the others. Tolerance is `1/VIF`. Guide: 1 to 5 moderate; above 5 (some use 10) high.

## Remedies

- Collect more data.
- Drop one of the correlated features, or combine them into one.
- **[[Ridge Regression]]** (stabilizes `X^T X + lambda I`).
- **PCA / partial least squares**: regress on uncorrelated components ([[Principal Component Analysis]]).
