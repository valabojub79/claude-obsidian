---
type: source
title: "SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1609.05473"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - gan
  - reinforcement-learning
  - generative
  - nlp
status: ingested
address: c-000289
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Professor Forcing - A New Algorithm for Training Recurrent Networks]]"
  - "[[An Actor-Critic Algorithm for Sequence Prediction]]"
  - "[[Generative Adversarial Networks]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/seq-gan.md]]"
---

# SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient

[Paper](https://arxiv.org/abs/1609.05473) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Yu et al. train a GAN for **discrete sequences**. The generator RNN is an RL policy (state = prefix, action = next token); a CNN **discriminator's** score on the finished sequence is the reward, and **Monte Carlo rollouts** complete partial sequences to estimate intermediate rewards. Trained with policy gradient (REINFORCE).

## Key points

- Addresses **exposure bias** in MLE, and needs no task metric (BLEU) or human labels.
- Alternation hyperparameters: g-steps, d-steps and `k` (discriminator epochs per batch of samples). They strongly affect stability; bad settings are barely better than MLE.
- Synthetic oracle task: a random LSTM generates 10k sequences of length 20 as "real data", which allows exact NLL evaluation. SeqGAN beats MLE, scheduled sampling and PG-BLEU.
- Real tasks: Chinese poems, Obama speeches, music. Beats MLE (most clearly on poems).

## Critique (Denny Britz)

Great paper, and the synthetic oracle is a neat evaluation idea. Real tasks lack a PG-BLEU comparison. Why do poems benefit so much more than the other tasks?
