---
type: concept
title: "Weight Initialization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000203
related:
  - "[[Vanishing and Exploding Gradients]]"
  - "[[Activation Functions]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Techniques/Weight Initialization/Weight Initialization.md]]"
---

# Weight Initialization

## Break symmetry

If all weights start equal (say zero), every hidden unit computes the same function and receives the same update, forever. So initialize `W[l]` **randomly**; biases can start at zero. Zero init is fine for [[Logistic Regression]] (no hidden units, convex cost).

## Keep it small, but the right size

Large weights push sigmoid or tanh into saturation and slow learning. Course 1 uses `randn * 0.01` for shallow nets. For deep nets, scale by fan-in so the variance of `z = sum w_i x_i` stays near 1:

| Scheme | Variance of W[l] | Best with |
|--------|------------------|-----------|
| **He** | `2 / n[l-1]` | ReLU |
| **Xavier / Glorot** | `1 / n[l-1]` | tanh |
| Glorot (avg fan) | `2 / (n[l-1] + n[l])` | tanh |

```python
W = np.random.randn(n_l, n_prev) * np.sqrt(2 / n_prev)   # He
```

The numerator can itself be tuned, but late in the search. Good init plus ReLU is a strong, partial fix for [[Vanishing and Exploding Gradients]].

## Related

- AI-Notes perspective: see the section below.
- Frameworks: TensorFlow 1.x `xavier_initializer`; PyTorch `kaiming_normal_`.

## AI-Notes perspective: why not zero or constant?

[[ai-notes|AI-Notes]] works through a 2-input, 1-hidden-layer example:

- **All zeros with ReLU or tanh**: hidden outputs are 0, so gradients are 0 and **no learning at all**.
- **All zeros with sigmoid**: every hidden unit outputs 0.5 and gets identical gradients, so the network behaves like **one neuron** and can't learn non-linear patterns.
- **Any constant**: same symmetry problem.
- **Plain standard normal**: too small means vanishing gradients; too large means exploding. So **scale by fan-in and fan-out**.

Goal: keep activation variance roughly constant across layers.

```python
std = np.sqrt(2 / (n_in + n_out))   # Xavier/Glorot (normal), for sigmoid/tanh
std = np.sqrt(2 / n_in)             # He, for ReLU family
W = np.random.normal(0, std, size=(n_in, n_out))
```

(The LISA MLP tutorial uses the **uniform** Glorot variant: `U[-sqrt(6/(fan_in+fan_out)), +sqrt(6/(fan_in+fan_out))]`, which has the same variance.)
