---
type: concept
title: "Dropout"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - regularization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000149
related:
  - "[[Regularization]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Techniques/Dropout.md]]"
---

# Dropout

On each training iteration, randomly zero each hidden unit with probability `1 - keep_prob`. Every step trains a different thinned network, which regularizes the whole.

## Inverted dropout (the standard implementation)

```python
d3 = np.random.rand(*a3.shape) < keep_prob   # mask
a3 = a3 * d3                                 # drop
a3 = a3 / keep_prob                          # rescale to keep E[a3] unchanged
```

- Use the same mask `d3` in the forward and backward pass of that iteration; draw a new one next iteration.
- **No dropout at test time.** Because of the `/ keep_prob` scaling, no test-time correction is needed.

## Intuitions

1. Each step trains a smaller network, which regularizes.
2. A unit can't rely on any single input, so it spreads its weights, an effect similar to L2 shrinkage.

## Practical notes

- `keep_prob` can differ per layer: lower for big layers that overfit, near 1.0 for the input layer.
- Heavily used in computer vision, where inputs are huge and data is always scarce.
- Downside: `J` is no longer well defined, so the cost curve is noisy. Debug with `keep_prob = 1`, confirm `J` falls monotonically, then turn dropout back on. The same goes for [[Gradient Checking]].

Original paper: Srivastava et al. 2014.

## AI-Notes perspective

[[ai-notes|AI-Notes]] describes dropout as training a different thinned network each step, an implicit **ensemble** that smooths the decision boundary. It explains classic (non-inverted) dropout: at test time multiply weights by `(1 - p)`, because each weight was active only that fraction of the time.

> [!contradiction] Who scales, and when?
> The AI-Notes page says Keras multiplies weights by `(1-p)` at test time. Keras (like PyTorch) actually implements **inverted dropout**: it scales surviving activations by `1/(1-p)` **during training**, and does nothing at inference. Both give the same expected activations, as DLAI's code above shows. Note also that Keras `Dropout(rate)` takes the **drop** probability, while DLAI's `keep_prob` is the keep probability.

Keras usage: `Dense(...)` then `Dropout(0.5)` after each hidden layer.
