---
type: concept
title: "Regression Analysis"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - mathematics
  - statistics
  - regression
  - inference
complexity: advanced
domain: mathematics
status: developing
address: c-000353
related:
  - "[[Linear Regression]]"
  - "[[Regression Metrics]]"
  - "[[T Test]]"
  - "[[Confidence Interval]]"
  - "[[Multicollinearity]]"
sources:
  - "[[.raw/repos/AI-Notes/Mathematics/Statistics/Regression Analysis.md]]"
---

# Regression Analysis

The **statistical-inference** view of [[Linear Regression]]: not just predicting, but asking whether relationships are real, how strong they are, and how certain the estimates are. From [[ai-notes|AI-Notes]] (CampusX).

## Prediction vs inference

- **Prediction**: estimate future outputs (stock prices, demand).
- **Inference**: understand *why*: which features matter and how (house-price drivers, loan eligibility).
- **Black-box** models (neural nets) predict well but explain poorly; **white-box** models (linear regression, trees) explain well.

Every ML problem is a **statistical inference problem**: we only ever have a sample, and there's always unexplained "hidden variance" (irreducible noise), so the true population relationship can't be recovered exactly.

## Decomposing variance

```
TSS = ESS + RSS
TSS = sum (y - y_bar)^2        total variance
ESS = sum (y_hat - y_bar)^2    explained by the model
RSS = sum (y - y_hat)^2        residual / unexplained
R^2 = ESS / TSS = 1 - RSS / TSS
```

R^2 and **adjusted R^2** measure the strength of the overall relationship; see [[Regression Metrics]] for the formula corrections.

## F-test: is the model significant at all?

H0: all slope coefficients are 0. H1: at least one isn't.

```
F = (ESS / p) / (RSS / (n - p - 1))      # p = number of predictors
```

(The source divides RSS by ESS, which is inverted.) A large F with a small p-value means the model explains significantly more than the mean. Assumes normally distributed residuals.

## t-tests: does each feature matter?

For each coefficient: H0 `b_j = 0`.

```
t_j = b_j / SE(b_j),   df = n - p - 1,   p-value from the t distribution (two-tailed)
```

A small p means the feature is significant. (The source says "divide t by df to get p", which is wrong: the p-value comes from the t-distribution's tail area.) See [[T Test]].

## Confidence intervals for coefficients

Coefficients are point estimates that vary by sample, so report `b_j +/- t* x SE(b_j)` ([[Confidence Interval]]).

## Diagnostics (statsmodels summary)

- **Omnibus** and **Jarque-Bera**: normality of residuals.
- **Durbin-Watson**: autocorrelation of residuals (about 2 is good).
- Also check linearity, homoscedasticity and [[Multicollinearity]] (VIF).
