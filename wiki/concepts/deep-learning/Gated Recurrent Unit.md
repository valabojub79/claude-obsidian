---
type: concept
title: "Gated Recurrent Unit"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - rnn
  - sequence-models
complexity: advanced
domain: deep-learning
status: developing
address: c-000155
related:
  - "[[Long Short-Term Memory]]"
  - "[[Recurrent Neural Networks]]"
  - "[[Vanishing and Exploding Gradients]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/GRU.md]]"
---

# Gated Recurrent Unit (GRU)

Cho et al. 2014; Chung et al. 2014. An RNN cell with a **memory cell** `c<t>` and gates that decide when to overwrite it, which lets information (and gradients) survive across many steps.

## Simplified GRU

```
c_tilde<t> = tanh( W_c [c<t-1>, x<t>] + b_c )          # candidate
Gamma_u    = sigmoid( W_u [c<t-1>, x<t>] + b_u )       # update gate
c<t>       = Gamma_u * c_tilde<t> + (1 - Gamma_u) * c<t-1>
a<t>       = c<t>
```

All products are element-wise; `c`, `c_tilde`, `Gamma_u` all have shape `(n_a, 1)`.

**Intuition** ("The cat, which already ate ..., was full"): `Gamma_u` is about 1 at "cat" (store "singular"), about 0 for the words in between (keep it), and the memory is consumed at "was". When `Gamma_u` is about 0, `c<t>` is about `c<t-1>`, so gradients pass through almost unchanged. That is why GRUs resist vanishing gradients.

## Full GRU

Adds a **relevance gate** `Gamma_r`:

```
Gamma_r    = sigmoid( W_r [c<t-1>, x<t>] + b_r )
c_tilde<t> = tanh( W_c [Gamma_r * c<t-1>, x<t>] + b_c )
```

Why this exact design? Researchers tried many variants; GRU and LSTM are the two that have proven robust across problems.

## GRU vs LSTM

GRU has two gates (simpler, faster, easier to scale up); [[Long Short-Term Memory]] has three (more powerful and flexible, the historical default). Neither is universally better.

## AI-Notes perspective

[[ai-notes|AI-Notes]] presents GRU as a simplification of the LSTM: **2 gates and 1 state** instead of 3 gates and 2 states.

- **Reset gate** `r_t = sigmoid(W [h_{t-1}, x_t])`: how much of `h_{t-1}` to use when forming the candidate `h~_t = tanh(W [r_t * h_{t-1}, x_t])`. It is DLAI's relevance gate `Gamma_r`.
- **Update gate** `z_t`: balances the candidate against the old state. High `z_t` favors new information. It is DLAI's `Gamma_u`.
- Unidirectional, like any RNN; use a **bidirectional GRU** when future context matters.

> [!contradiction] Date
> AI-Notes says GRU was "introduced in 2016". It was introduced by Cho et al. in **2014**, in [[Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation]].
