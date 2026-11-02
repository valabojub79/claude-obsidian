---
type: concept
title: "Generative Adversarial Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - generative
  - gan
complexity: advanced
domain: deep-learning
status: developing
address: c-000156
related:
  - "[[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]]"
  - "[[Neural Style Transfer]]"
  - "[[deep-learning-reading-list|Deep Learning Reading List 2013-2018]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/README.md]]"
---

# Generative Adversarial Networks (GANs)

Goodfellow et al., 2014. Two networks play a minimax game:

- a **generator** `G(z)` maps noise to fake samples;
- a **discriminator** `D(x)` estimates whether `x` is real.

```
min_G max_D  E_x[log D(x)] + E_z[log(1 - D(G(z)))]
```

`G` improves by fooling `D`, and `D` by catching `G`. At equilibrium, `G`'s distribution matches the data.

> [!gap] No dedicated source
> None of the four repos has a GAN deep-dive. This page connects what they do contain.

## What the sources say

- **Ian Goodfellow interview** (DLAI Course 1): GANs are his creation; **stabilizing training** is the key open problem ([[DLAI Course 1 - Neural Networks and Deep Learning]]).
- **GANs for discrete sequences** need policy gradients, because you can't backprop through sampled tokens: [[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]]. Matching *hidden states* instead sidesteps this: [[Professor Forcing - A New Algorithm for Training Recurrent Networks]].
- **Adversarial imitation**: GAIL with domain confusion ([[Third-Person Imitation Learning]]).
- **Reading list landmarks** (22 GAN papers in [[deep-learning-reading-list|Deep Learning Reading List 2013-2018]]): DCGAN (convolutional architecture guidelines), *Improved Techniques for Training GANs* (feature matching, minibatch discrimination), InfoGAN (disentangled codes), pix2pix and StarGAN (conditional image-to-image), WGAN (Wasserstein loss for stability), Progressive Growing of GANs (high resolution).

## Relatives

[[Neural Style Transfer]] (optimization-based image generation), VAEs ([[Generating Sentences from a Continuous Space]]; [[Autoencoders]]), autoregressive models (PixelCNN, WaveNet), and diffusion models (today's dominant image generators), which typically use the U-Net from [[LISA Tutorial - Semantic Segmentation FCN and U-Net]].
