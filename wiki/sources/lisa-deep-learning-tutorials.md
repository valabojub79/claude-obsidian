---
type: source
title: "LISA Deep Learning Tutorials"
source_type: repository
author: "LISA lab (now Mila), Université de Montréal"
date_published: 2017-01-01
date_ingested: 2026-11-02
created: 2026-11-02
updated: 2026-11-02
url: "https://github.com/lisa-lab/DeepLearningTutorials"
commit: 11c465105026cf87573937fc2d35ab7543678698
license: BSD-3-Clause
confidence: high
tags:
  - source
  - deep-learning
  - tutorial
  - theano
status: ingested
address: c-000125
related:
  - "[[Yoshua Bengio]]"
  - "[[Theano]]"
  - "[[Deep Learning]]"
  - "[[Unsupervised Pretraining]]"
sources:
  - ".raw/repos/DeepLearningTutorials/"
key_claims:
  - "Greedy layer-wise unsupervised pretraining (SdA, DBN) beats a plain MLP on MNIST (1.3% vs 1.65% test error)"
  - "Noise in denoising autoencoders is what makes the learned features useful"
  - "CD-1 works surprisingly well for training RBMs; PCD gives better generative models"
  - "Fully convolutional encoder-decoders with skip connections handle segmentation at any input size"
---

# LISA Deep Learning Tutorials

The deeplearning.net tutorials from Yoshua Bengio's LISA lab (now **Mila**): Sphinx docs (`doc/*.txt`) plus runnable Theano code (`code/`). It was the canonical hands-on deep learning curriculum of about 2010 to 2016, and documents the **unsupervised pretraining era**. BSD licensed. Snapshot at `11c4651`, stored locally (gitignored) in `.raw/repos/DeepLearningTutorials/`.

> [!stale] Theano is discontinued
> Theano stopped development in 2017 (successors: Aesara, PyTensor), and some tutorials are Python 2 only. Read these for the **ideas and math**; reimplement in PyTorch or JAX to run them.

## Reading order and wiki pages

**Supervised (in order):**

1. [[LISA Tutorial - Getting Started]]: MNIST, NLL, MSGD, early stopping with patience.
2. [[LISA Tutorial - Logistic Regression]]: 7.49% test error.
3. [[LISA Tutorial - Multilayer Perceptron]]: 1.65%.
4. [[LISA Tutorial - Convolutional Networks LeNet]].

**Unsupervised and pretraining (any order):**

- [[LISA Tutorial - Denoising Autoencoders]], then [[LISA Tutorial - Stacked Denoising Autoencoders]] (1.30%).
- [[LISA Tutorial - Restricted Boltzmann Machines]], then [[LISA Tutorial - Deep Belief Networks]] (1.34%).
- [[LISA Tutorial - Hybrid Monte Carlo Sampling]] (toward mcRBM).
- Contractive autoencoders: code only (`cA.py`).

**Sequences:**

- [[LISA Tutorial - RNN for Slot Filling]]: ATIS, 94.48% F1.
- [[LISA Tutorial - LSTM Sentiment Analysis]]: IMDB.
- [[LISA Tutorial - RNN-RBM Polyphonic Music]].

**Medical image segmentation (Lasagne):**

- [[LISA Tutorial - Semantic Segmentation FCN and U-Net]].
- [[LISA Tutorial - 1D Segmentation of Cortical Layers]].

## Cross-cutting concept pages created

[[Multilayer Perceptron]], [[Autoencoders]], [[Unsupervised Pretraining]], [[Energy-Based Models]], [[Semantic Segmentation]]

## Utilities

`tile_raster_images` reshapes each row of a minibatch, or each column of a weight matrix, into a 2D tile and lays them out in a grid, which is how the tutorials visualize filters and samples. It neglects biases and rescales weights to [0, 1], so it "doesn't tell the whole story".

## Connections

- Complements [[deeplearning-ai-summary|DeepLearning.ai Summary]]: DLAI explains modern supervised practice (2017); LISA shows the pretraining era and the probabilistic models DLAI skips (RBMs, DBNs, HMC).
- Many LISA authors' papers appear in [[deeplearning-papernotes|Deep Learning Paper Notes]].
