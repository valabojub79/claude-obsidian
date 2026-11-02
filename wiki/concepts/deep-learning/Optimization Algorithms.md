---
type: concept
title: "Optimization Algorithms"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000186
related:
  - "[[Gradient Descent]]"
  - "[[Mini-Batch Gradient Descent]]"
  - "[[Hyperparameter Tuning]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Techniques/Optimizers.md]]"
---

# Optimization Algorithms

Improvements on plain [[Gradient Descent]] covered in DLAI Course 2, week 2.

## Exponentially weighted averages (EWA)

```
v_t = beta * v_{t-1} + (1 - beta) * theta_t
```

Roughly averages the last `1 / (1 - beta)` values (`beta = 0.9` gives about 10, `0.98` about 50). It needs O(1) memory, unlike a moving window.

**Bias correction:** since `v_0 = 0`, early values are too low. Divide by `(1 - beta^t)`. It mostly matters in the first few steps.

## Momentum

Apply the EWA to gradients and step along the smoothed direction:

```
vdW = beta*vdW + (1-beta)*dW
W  -= alpha * vdW
```

This damps oscillations across the ravine and speeds progress along it. `beta = 0.9` is a robust default; people rarely bother with bias correction here.

## RMSprop

Divide by a running RMS of the gradient, per parameter:

```
sdW = beta*sdW + (1-beta)*dW**2
W  -= alpha * dW / (sqrt(sdW) + eps)
```

Steep, oscillating directions get small steps and flat ones get large steps, which allows a larger `alpha`. Introduced by Hinton in a Coursera lecture.

## Adam (Adaptive Moment Estimation)

Momentum plus RMSprop, with bias correction on both:

```
v = b1*v + (1-b1)*dW;      s = b2*s + (1-b2)*dW**2
v_hat = v/(1-b1**t);       s_hat = s/(1-b2**t)
W -= alpha * v_hat / (sqrt(s_hat) + eps)
```

Defaults: `b1 = 0.9`, `b2 = 0.999`, `eps = 1e-8`; tune only `alpha`. A strong default across architectures. Paper: Kingma & Ba, 2015 (no note in the paper repo).

## Learning-rate decay

Shrink `alpha` over time so mini-batch GD settles closer to the minimum:

- `alpha = alpha0 / (1 + decay_rate * epoch)`
- `alpha = 0.95^epoch * alpha0` (exponential)
- `alpha = k / sqrt(epoch) * alpha0`
- Discrete staircase, or manual adjustment.

Ng ranks decay low on the tuning priority list.

## Local optima and plateaus

In high dimensions, a zero-gradient point is almost always a **saddle point**, not a bad local minimum: being a minimum would require curving up in every one of thousands of directions. The real problem is **plateaus**, long flat regions that momentum, RMSprop and Adam help cross.

## Related

- AI-Notes perspective: see the section below.

## AI-Notes perspective: why study optimizers?

[[ai-notes|AI-Notes]] motivates optimizers with three weaknesses of plain (mini-batch) gradient descent: **sensitivity to the learning rate**, **getting stuck** in local minima (in practice saddle points and plateaus, per DLAI above), and **one learning rate for all parameters**. Momentum, RMSprop and Adam address these. The source page is unfinished beyond this motivation.
