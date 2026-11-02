---
type: concept
title: "LISA Tutorial - Getting Started"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
complexity: beginner
domain: deep-learning
status: developing
address: c-000168
related:
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[Mini-Batch Gradient Descent]]"
  - "[[Regularization]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/gettingstarted.txt]]"
---

# LISA Tutorial: Getting Started

The shared foundation for every tutorial in [[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]: datasets, notation, the training loop, and Theano practicalities.

## MNIST setup

- 60,000 train and 10,000 test digits, 28x28 grayscale. The tutorials split the official train set into **50,000 train and 10,000 validation**.
- Pickled as `(train, valid, test)`, each `(images: 784 floats in [0,1], labels 0 to 9)`.
- **Store the data in Theano shared variables** so it is copied to the GPU once; each minibatch is then a slice by index. Copying per batch would erase the GPU's speed-up. Labels are stored as `floatX` and cast to `int32`, because GPU storage had to be float.

## Losses

- **Zero-one loss** `sum I[f(x) != y]` is what we care about but isn't differentiable.
- Minimize **negative log-likelihood** `NLL = -sum log P(Y = y_i | x_i, theta)` as a differentiable surrogate. They're correlated but can move in opposite directions on validation.

## Minibatch SGD (MSGD)

GD uses all data per step; SGD uses one example; **MSGD** uses a batch `B`. Variance reduction and SIMD help most going from B=1 to 2 and then fade fast; huge `B` wastes compute on gradient precision instead of more steps. The tutorials use `B = 20`, "almost arbitrary". With a fixed number of epochs, `B` changes the number of updates, so retune other hyperparameters when you change it. See [[Mini-Batch Gradient Descent]].

## Regularization

- **L1/L2**: `E = NLL + lambda * ||theta||_p^p`; `p = 2` is "weight decay". It encodes an Occam's-razor preference for smooth solutions; empirically it helps most on small datasets.
- **Early stopping with patience**: evaluate on validation every `validation_frequency` steps; whenever validation improves "significantly" (by more than `improvement_threshold`, say 0.995), extend `patience` geometrically (`patience = max(patience, iter * patience_increase)`); stop when patience runs out. Report the test score of the best-validation model.

See also [[Regularization]].

## Theano tips

- Save models by **pickling the numpy arrays** from shared variables, not compiled Theano functions (internal APIs change).
- Training scripts should save intermediate models; a **separate** script visualizes them, so you can investigate later without retraining.
