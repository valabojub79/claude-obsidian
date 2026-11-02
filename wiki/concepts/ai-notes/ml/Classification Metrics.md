---
type: concept
title: "Classification Metrics"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - machine-learning
  - evaluation
complexity: beginner
domain: machine-learning
status: developing
address: c-000358
related:
  - "[[Regression Metrics]]"
  - "[[Evaluation Metrics and Dev Sets]]"
  - "[[Imbalanced Data]]"
sources:
  - "[[.raw/repos/AI-Notes/Machine Learning/Performance Metrics/Classification Metrics.md]]"
---

# Classification Metrics

From [[ai-notes|AI-Notes]]. See also DLAI's single-number-metric advice in [[Evaluation Metrics and Dev Sets]].

## Accuracy

`correct / total`. Two flaws:

1. **Misleading under class imbalance**: 98 A and 2 B means "always predict A" scores 98%. See [[Imbalanced Data]].
2. It doesn't say **which** errors occur.

"Good" accuracy is problem-dependent: 95% may be unacceptable for brain-tumor detection, but fine for rain forecasting.

## Confusion matrix

|  | Predicted + | Predicted - |
|-|-------------|-------------|
| **Actual +** | TP | FN (**Type II**) |
| **Actual -** | FP (**Type I**) | TN |

Which error is worse depends on the problem. **Spam filter**: an FP (real mail sent to spam) is worse. **Disease screening**: an FN (sick person missed) is worse.

## Precision, recall, F1

```
Precision = TP / (TP + FP)     # "of predicted positives, how many are right?" Use when FP is costly
Recall    = TP / (TP + FN)     # "of actual positives, how many did we catch?" Use when FN is costly
F1        = 2PR / (P + R)      # harmonic mean, when unsure which matters more
```

Why the **harmonic** mean: it punishes imbalance. P = 1.0 and R = 0.0 gives F1 = 0, whereas the arithmetic mean would say 0.5. Generalization: F-beta weights recall `beta` times as much as precision.

## ROC-AUC

(Unfinished in the source.) ROC plots TPR (recall) against FPR (`FP/(FP+TN)`) across thresholds; AUC is the probability that a random positive outranks a random negative. 0.5 is random, 1.0 perfect. Under heavy imbalance, also check **PR-AUC**.

Multiclass: macro, micro or weighted averages of per-class P, R and F1.
