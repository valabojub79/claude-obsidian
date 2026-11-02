---
type: concept
title: "Multi-Task Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - transfer-learning
complexity: intermediate
domain: deep-learning
status: developing
address: c-000182
related:
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# Multi-Task Learning

One network learns several tasks **at once**, sharing lower layers. (Contrast: [[Transfer Learning]] is sequential, A then B.)

## Example

An autonomous-driving image can contain pedestrians, cars, stop signs and traffic lights. Use 4 sigmoid outputs (not softmax: several can be true together), so `Y` has shape `(4, m)`:

```
J = (1/m) * sum_i sum_j L(y_hat_ij, y_ij)          # per-label logistic loss
```

**Missing labels** (`?`) are fine: sum only over labeled `j`.

## When it makes sense

1. Tasks benefit from shared low-level features.
2. Data per task is similar in amount; each task gets a boost from the others' data.
3. You can train a network big enough for all the tasks. If you can, multi-task usually beats separate networks.

In practice transfer learning is used far more often; object detection is the big multi-task exception.
