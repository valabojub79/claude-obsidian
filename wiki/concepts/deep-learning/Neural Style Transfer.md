---
type: concept
title: "Neural Style Transfer"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - computer-vision
  - generative
complexity: advanced
domain: deep-learning
status: developing
address: c-000184
related:
  - "[[Convolutional Neural Networks]]"
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/4- Convolutional Neural Networks/Readme.md]]"
---

# Neural Style Transfer

Gatys et al., 2015. Given a **content** image C and a **style** image S, synthesize a **generated** image G with C's content painted in S's style. It optimizes **pixels**, not weights, using a frozen pretrained CNN (VGG) as the feature extractor, a form of [[Transfer Learning]].

## What CNN layers see (Zeiler & Fergus 2013)

For a unit, find the image patches that maximize it. Layer 1 units see small patches (edges, color blobs); deeper units see larger receptive fields (textures, then object parts, then whole objects such as dogs, wheels or text).

## Cost

```
J(G) = alpha * J_content(C, G) + beta * J_style(S, G)
```

Initialize G randomly (or as C plus noise) and run gradient descent on G's pixels.

### Content cost

Pick a **middle** layer `l` (not too shallow, which copies pixels; not too deep, which keeps only "a dog exists"):

```
J_content = 1/2 * || a[l](C) - a[l](G) ||^2
```

### Style cost

Style is the **correlation between channels**: which features co-occur (for example "vertical texture" with "orange tint"). Gram matrix at layer `l`, shape `n_c x n_c`:

```
F = reshape(a[l], (n_c, n_H * n_W))
G_gram[l] = F @ F.T
J_style[l] = 1 / (2 n_H n_W n_c)^2 * || G_gram[l](S) - G_gram[l](G) ||_F^2
J_style = sum_l lambda[l] * J_style[l]          # several layers: low and high-level style
```

## TensorFlow assignment recipe

Load C and S, initialize G, load VGG-16 or 19, compute content and style costs through the network, total cost, Adam on G for many iterations.

## Related

Learned generators replaced optimization later: see [[Generative Adversarial Networks]].
