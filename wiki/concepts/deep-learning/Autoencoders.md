---
type: concept
title: "Autoencoders"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - unsupervised
  - representation-learning
complexity: intermediate
domain: deep-learning
status: developing
address: c-000131
related:
  - "[[LISA Tutorial - Denoising Autoencoders]]"
  - "[[LISA Tutorial - Stacked Denoising Autoencoders]]"
  - "[[Unsupervised Pretraining]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/dA.txt]]"
---

# Autoencoders

A network trained to reproduce its input through a **code** (hidden representation):

```
y = s(W x + b)          # encoder
z = s(W' y + b')        # decoder; "tied weights" if W' = W^T
```

Loss: squared error `||x - z||^2`, or cross-entropy `-sum [x_k log z_k + (1-x_k) log(1-z_k)]` for binary or probability-valued inputs.

## Relation to PCA

With one **linear** hidden layer and MSE, the `k` hidden units span the first `k` principal components. Non-linear (and stacked, deep) autoencoders capture multi-modal structure that PCA can't. See [[Principal Component Analysis]].

## Why it generalizes

The code is a lossy compression that works well only for inputs resembling the training data. That's the sense in which an autoencoder "learns the distribution": low reconstruction error on in-distribution data, high error on random inputs. That property is also the basis of autoencoder **anomaly detection**.

## Avoiding the identity map

An over-complete autoencoder (more hidden units than inputs) could just copy. Countermeasures:

- **Implicit regularization**: SGD with early stopping acts like L2. Perfect reconstruction needs tiny encoder and huge decoder weights, which regularization discourages.
- **Sparsity** penalties (Ranzato 2007, Lee 2008).
- **Noise**: [[LISA Tutorial - Denoising Autoencoders|denoising autoencoders]], or the stochasticity of [[LISA Tutorial - Restricted Boltzmann Machines|RBMs]].
- **Contractive** penalty (cA, code-only in the LISA repo).

## Descendants

Stacked autoencoders for [[Unsupervised Pretraining]] (2006-2010); **variational autoencoders** (generative models); masked autoencoding (BERT, MAE) is the denoising idea at scale. (AI-Notes' autoencoder page is an empty stub.)
