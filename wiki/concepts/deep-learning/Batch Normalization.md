---
type: concept
title: "Batch Normalization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - optimization
complexity: intermediate
domain: deep-learning
status: developing
address: c-000134
related:
  - "[[Input Normalization]]"
  - "[[Regularization]]"
  - "[[Batch Normalization - Accelerating Deep Network Training]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Techniques/Batch Normalization.md]]"
---

# Batch Normalization

Ioffe and Szegedy (2015). Normalize each hidden layer's pre-activations `Z[l]` over the mini-batch, then let the network rescale them:

```
mu      = mean(z_i)
sigma2  = var(z_i)
z_norm  = (z_i - mu) / sqrt(sigma2 + eps)
z_tilde = gamma * z_norm + beta          # gamma, beta are learned
```

If `gamma = sqrt(sigma2 + eps)` and `beta = mu`, BN reduces to the identity, so it can't hurt expressiveness. Normalizing `Z` (before the activation) is the common choice.

## In a network

- Parameters become `W[l], gamma[l], beta[l]`. Drop `b[l]`: mean subtraction cancels it, and `beta[l]` takes its role.
- `gamma[l]` and `beta[l]` have shape `(n[l], 1)` and are updated by any optimizer (GD, momentum, Adam).
- Applied per mini-batch. Frameworks provide it, for example `tf.nn.batch_normalization` or PyTorch `BatchNorm1d` / `BatchNorm2d`.

## Why it works

1. Same as [[Input Normalization]]: a rounder cost surface at every layer.
2. **Reduces covariate shift** in hidden layers: later layers see inputs with a stable mean and variance even as earlier weights change, so layers learn more independently.
3. **Slight regularization:** mini-batch statistics add noise, a bit like [[Dropout]]. Larger batches give less noise and less regularization. Don't use BN *as* a regularizer.

## Test time

A single example has no batch statistics. Keep an exponentially weighted running average of `mu` and `sigma2` during training (see [[Optimization Algorithms]]) and use those at inference. Frameworks do this automatically.

## Related

- Paper page: [[Batch Normalization - Accelerating Deep Network Training]].
- AI-Notes perspective: see the section below.

## AI-Notes perspective

[[ai-notes|AI-Notes]] frames BN around **covariate shift** (input distributions differ between train and test) and **internal covariate shift** (each layer's input distribution keeps moving as earlier weights change, so the network needs many epochs to adapt). Procedure: compute pre-activations, batch mean and variance, normalize, scale and shift with learnable `gamma` and `beta`, then activate. Why the scale and shift: mean 0 and variance 1 isn't optimal for every layer.

Keras pattern (BN between the linear layer and the activation):

```python
model.add(Dense(64, input_shape=(128,)))
model.add(BatchNormalization())
model.add(Activation('relu'))
```
