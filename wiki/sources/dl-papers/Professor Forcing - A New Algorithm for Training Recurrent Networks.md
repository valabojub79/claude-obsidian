---
type: source
title: "Professor Forcing - A New Algorithm for Training Recurrent Networks"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.09038"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - rnn
  - gan
  - training
status: ingested
address: c-000278
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]]"
  - "[[An Actor-Critic Algorithm for Sequence Prediction]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/professor-forcing.md]]"
---

# Professor Forcing - A New Algorithm for Training Recurrent Networks

[Paper](https://arxiv.org/abs/1610.09038) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Lamb, Goyal et al. address the train/test mismatch of **teacher forcing** with a GAN-style discriminator. It tries to tell teacher-forced runs from free-running runs, based on hidden states plus outputs; the generator RNN is trained (alongside MLE) to make the free-running dynamics indistinguishable from the teacher-forced ones. It acts as a regularizer and improves samples and generalization.

## Key points

- Generator: GRU with softmax; behavior = pre-tanh GRU states plus softmax output. Discriminator: BiGRU with a 3-layer MLP.
- Trick: backprop the discriminator signal into the generator only when discriminator accuracy is **between 75% and 99%**. Adam.
- Results: PTB character LM 1.48 bits/char; sequential MNIST NLL 79.58 (second to PixelCNN); handwriting and music rated better by humans, especially for long sequences. **No effect on word-level LM.**
- t-SNE confirms hidden-state distributions become more similar.

## Critique (Denny Britz)

Very clearly written. Why match hidden states and not just outputs? (Answer from a reader: outputs are discrete, so a GAN over them needs policy gradients as in [[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient|SeqGAN]], which is harder to converge.) Which regularizer term matters? How hard is it to balance generator and discriminator? Try it on translation.
