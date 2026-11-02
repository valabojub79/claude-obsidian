---
type: concept
title: "Evaluation Metrics and Dev Sets"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: beginner
domain: deep-learning
status: developing
address: c-000153
related:
  - "[[Train Dev Test Split]]"
  - "[[Orthogonalization]]"
  - "[[Classification Metrics]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Evaluation Metrics and Dev Sets

## Single-number evaluation metric

Pick one number up front so you can rank ideas instantly. Precision and recall separately don't say whether A (95% P, 90% R) beats B (98% P, 85% R); their harmonic mean does:

```
F1 = 2 / (1/P + 1/R)
```

Cat example (5 cats, 5 non-cats; 3 TP, 1 FP, 2 FN, 4 TN): P = 3/4, R = 3/5, accuracy = 7/10. Metric details: [[Classification Metrics]].

## Optimizing vs satisficing metrics

With N criteria, **optimize 1** and treat the other **N-1 as thresholds**:

```
maximize  F1
subject to latency < 100 ms,  false-wake-ups <= 1 per 24h
```

## Dev and test sets define the target

- Same distribution, reflecting the data you expect and care about.
- Size: just big enough for confidence (see [[Train Dev Test Split]]).

## When to change the metric

If the metric and dev set rank models differently from your users, the **target** is wrong. Example: Algorithm A has 3% error but lets pornographic images through as "cats"; B has 5% error and doesn't. Users prefer B. Fix the metric with weights:

```
error = (1 / sum w_i) * sum w_i * [y_pred_i != y_i],   w_i = 10 if x_i is porn, else 1
```

Likewise, if users upload blurry phone photos but your dev set holds crisp web photos, change the dev set. Rule: **if doing well on metric plus dev set doesn't mean doing well in the application, change them.**
