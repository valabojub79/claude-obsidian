---
type: concept
title: "LISA Tutorial - Deep Belief Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - unsupervised
  - generative
complexity: advanced
domain: deep-learning
status: developing
address: c-000166
related:
  - "[[LISA Tutorial - Restricted Boltzmann Machines]]"
  - "[[Unsupervised Pretraining]]"
  - "[[LISA Tutorial - Stacked Denoising Autoencoders]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/DBN.txt]]"
---

# LISA Tutorial: Deep Belief Networks (DBN)

Hinton, Osindero, Teh, 2006: the paper usually credited with restarting deep learning. Stack [[LISA Tutorial - Restricted Boltzmann Machines|RBMs]] and train them greedily.

## Model

```
P(x, h1, ..., hl) = ( prod_{k=0}^{l-2} P(h_k | h_{k+1}) ) * P(h_{l-1}, h_l)      # x = h0
```

The top two layers form an RBM (undirected); the lower layers are directed sigmoid belief nets.

## Greedy layer-wise training

1. Train RBM 1 on `x`.
2. Represent the data by mean activations `p(h1 = 1 | x)` or by samples.
3. Train RBM 2 on that, and so on.
4. Fine-tune: either a generative proxy for the DBN likelihood, or **supervised** (this tutorial): add logistic regression on top and backprop. Equivalent to initializing a deep MLP with RBM weights and hidden biases.

## Why greedy stacking works (variational bound)

```
log p(x) = KL(Q(h1|x) || p(h1|x)) + H[Q(h1|x)] + sum_h Q(h1|x) [log p(h1) + log p(x|h1)]
```

If `W2 = W1^T` initially, the KL term is 0. Freezing `W1` and training `W2` (a second RBM on `Q(h1|x)`) can then only **increase** the bound on likelihood. Each added layer improves a lower bound.

## MNIST result

3 x 1000 hidden units, 100 pre-training epochs (batch 10, about 500k unsupervised updates, lr 0.01), fine-tuning lr 0.1. **Test error 1.34%** (validation 1.27%) after 46 supervised epochs. Pre-training took 615 minutes on 4 cores. No regularization besides early stopping.

The code mirrors [[LISA Tutorial - Stacked Denoising Autoencoders|SdA]], with RBM instead of dA; the same "cache layer-k representations" speed trick applies.

## Historical note

Unsupervised pre-training was the key to training deep nets from 2006 to about 2011. ReLU, better initialization, dropout and BatchNorm made it unnecessary for supervised tasks. See [[Unsupervised Pretraining]].
