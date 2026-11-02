---
type: concept
title: "Vanishing and Exploding Gradients"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000201
related:
  - "[[Weight Initialization]]"
  - "[[Activation Functions]]"
  - "[[Residual Networks]]"
  - "[[Long Short-Term Memory]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Vanishing and Exploding Gradients

In a deep network, activations and gradients are products of many per-layer factors, so they can shrink or grow **exponentially in depth**.

## Toy example (DLAI)

Linear activations, `b = 0`, every `W[l] = c * I`:

```
y_hat = W[L] * (c*I)^(L-1) * x
```

- `c = 1.5` gives values that grow like `1.5^L` (explode).
- `c = 0.5` gives values that shrink like `0.5^L` (vanish).

The same happens to gradients. Vanishing gradients make early layers learn extremely slowly; exploding ones produce NaNs.

## Mitigations

| Fix | Where covered |
|-----|---------------|
| Careful init (He for ReLU, Xavier for tanh) | [[Weight Initialization]] |
| Non-saturating activations (ReLU) | [[Activation Functions]] |
| Skip connections | [[Residual Networks]] |
| [[Batch Normalization]] | Course 2 |
| Gradient clipping (for exploding) | [[Recurrent Neural Networks]] |
| Gated recurrent units | [[Gated Recurrent Unit]], [[Long Short-Term Memory]] |

RNNs are especially exposed because the same weight matrix is multiplied once per time step.

## Related

- AI-Notes' explanation (sigmoid derivative of at most 0.25) is merged into [[Multilayer Perceptron]].
