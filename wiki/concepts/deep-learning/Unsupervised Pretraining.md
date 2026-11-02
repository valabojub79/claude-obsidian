---
type: concept
title: "Unsupervised Pretraining"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - unsupervised
  - history
complexity: intermediate
domain: deep-learning
status: developing
address: c-000200
related:
  - "[[LISA Tutorial - Deep Belief Networks]]"
  - "[[LISA Tutorial - Stacked Denoising Autoencoders]]"
  - "[[Transfer Learning]]"
  - "[[Weight Initialization]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/SdA.txt]]"
---

# Unsupervised Pretraining

Initialize a deep network by training it **layer by layer without labels**, then fine-tune the whole network on the supervised task.

## Recipe (2006-2010 era)

1. Train layer 1 as an unsupervised model on the raw input: an RBM ([[LISA Tutorial - Deep Belief Networks|DBN]]) or a denoising autoencoder ([[LISA Tutorial - Stacked Denoising Autoencoders|SdA]]).
2. Feed its representation to layer 2, train that, and repeat.
3. Add a classifier on top and fine-tune everything with backprop.

On MNIST in the LISA tutorials: plain MLP 1.65%, SdA 1.30%, DBN 1.34% test error.

## Why it helped (Bengio, Erhan et al.)

- A data-dependent **initialization** that puts weights in a good basin, at a time when random init plus sigmoid made deep nets untrainable ([[Vanishing and Exploding Gradients]]).
- A **regularizer**: it biases the network toward features that model `p(x)`, which helps when labels are scarce.

## Why it faded

ReLU, Xavier and He init ([[Weight Initialization]]), [[Dropout]], [[Batch Normalization]], GPUs and big labeled datasets (ImageNet) made purely supervised deep training work from about 2012.

## Why it came back

The same idea at internet scale: self-supervised pretraining (word2vec, BERT's masked tokens, GPT's next-token prediction, MAE) followed by fine-tuning is today's dominant paradigm. See [[Transfer Learning]] and [[Large Language Models]].
