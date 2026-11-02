---
type: concept
title: "LISA Tutorial - Stacked Denoising Autoencoders"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - unsupervised
complexity: intermediate
domain: deep-learning
status: developing
address: c-000177
related:
  - "[[LISA Tutorial - Denoising Autoencoders]]"
  - "[[Unsupervised Pretraining]]"
  - "[[LISA Tutorial - Deep Belief Networks]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/SdA.txt]]"
---

# LISA Tutorial: Stacked Denoising Autoencoders (SdA)

Bengio 2007 (stacked autoencoders) and Vincent 2008 (denoising version). A deep network trained in two stages; see [[Unsupervised Pretraining]].

## Stage 1: greedy layer-wise pre-training (unsupervised)

Train layer 1 as a [[LISA Tutorial - Denoising Autoencoders|dA]] on the input. Then train layer 2 as a dA on layer 1's codes, and so on.

## Stage 2: supervised fine-tuning

Add a logistic regression layer on top, then train the **whole stack as an MLP** by backprop on labels. Only the encoder halves are kept.

## Two facades, shared parameters

The `SdA` class holds `sigmoid_layers` (MLP view) and `dA_layers` (autoencoder view) that **share** `W` and `b`. Pre-training uses the dA view; fine-tuning the MLP view. Hidden units are sigmoid, not tanh, here.

`pretraining_functions()` returns one compiled function per layer, taking `index`, `corruption` and `lr` (named by the Theano variable names, not the Python names: a gotcha).

## MNIST result

3 hidden layers; corruption 0.1, 0.2, 0.3 per layer; pretrain lr 0.001, fine-tune lr 0.1. **Test error 1.3%** (validation 1.39%). That's about 585 minutes of pre-training plus 444 minutes of fine-tuning on a single CPU thread in about 2010.

## Speed tip

After training layer k, push the whole dataset through once and store its codes as the training set for layer k+1. That avoids recomputing lower layers every epoch, at the cost of memory.
