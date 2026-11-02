---
type: concept
title: "Mini-Batch Gradient Descent"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000181
related:
  - "[[Gradient Descent]]"
  - "[[Optimization Algorithms]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Mini-Batch Gradient Descent

Split the training set into mini-batches `X{t}, Y{t}` and take a [[Gradient Descent]] step after each one. One pass over all mini-batches is an **epoch**.

```
for epoch in range(num_epochs):
    for t in range(num_batches):
        A, caches = forward(X{t})
        cost = compute_cost(A, Y{t})
        grads = backward(caches)
        update(params, grads)
```

## The spectrum

| Batch size | Name | Pros | Cons |
|-----------|------|------|------|
| `m` | Batch GD | Smooth, monotone cost | Very slow per step on big data |
| 1 | Stochastic GD | Instant progress | Noisy; loses vectorization; never settles |
| between | Mini-batch | Vectorized **and** frequent updates | Cost wiggles; oscillates near the minimum |

The mini-batch cost curve trends down but noisily; that's expected.

## Choosing the size

- Fewer than ~2,000 examples: just use batch GD.
- Otherwise powers of two: 64, 128, 256, 512 (memory alignment).
- The mini-batch must fit in CPU or GPU memory.
- It's a hyperparameter. Pair with learning-rate decay to settle closer to the optimum (see [[Optimization Algorithms]]).
