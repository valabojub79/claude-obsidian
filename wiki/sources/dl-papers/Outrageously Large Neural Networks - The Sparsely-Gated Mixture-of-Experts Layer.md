---
type: source
title: "Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer"
source_type: paper
year: 2017
url: "https://openreview.net/forum?id=B1ckMDqlg"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - scaling
  - conditional-computation
  - nmt
  - language-modeling
status: ingested
address: c-000275
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Adaptive Computation Time for Recurrent Neural Networks]]"
  - "[[Exploring the Limits of Language Modeling]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/mixture-experts.md]]"
---

# Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer

[Paper](https://openreview.net/forum?id=B1ckMDqlg) (2017) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Shazeer et al. add a **Sparsely-Gated Mixture-of-Experts** layer: up to thousands of feed-forward experts and a trainable gate that routes each example to the **top-k** experts. Parameters grow to **tens of billions** at nearly constant compute. State of the art on One Billion Word LM and WMT EN-FR and EN-DE.

## Key points

```
y = sum_i G(x)_i * E_i(x),   G(x) = softmax(topk(x W_g + noise))
```

- **Load balancing**: an extra loss keeps all experts used; otherwise a few dominate.
- **Shrinking batch problem**: each expert sees only a fraction of the batch. Fixes: combine batches across data-parallel replicas and time steps.
- Results: 1B-word LM perplexity 29.9 with 34B parameters (15 h on 128 K40s); EN-FR **40.56 BLEU** with 8.7B parameters.

## Critique (Denny Britz)

Like highway networks with sparse gates. Why not experts with *different* architectures? Wry note on the learning-rate schedule: warm up linearly, then decay with the inverse square root of the step (the same schedule the Transformer paper uses).

## Connections

The direct ancestor of today's MoE LLMs (Switch Transformer, Mixtral, DeepSeek-MoE).
