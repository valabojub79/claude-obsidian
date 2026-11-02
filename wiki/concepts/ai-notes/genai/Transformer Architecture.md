---
type: concept
title: "Transformer Architecture"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - attention
complexity: advanced
domain: generative-ai
status: developing
address: c-000338
related:
  - "[[Attention Mechanism]]"
  - "[[Large Language Models]]"
  - "[[Layer Normalization]]"
  - "[[Residual Networks]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/History Behind LLM.md]]"
---

# Transformer Architecture

Vaswani et al., 2017, *Attention Is All You Need* (listed in [[deep-learning-reading-list|Deep Learning Reading List 2013-2018]]). It removes recurrence: every layer lets each token attend to every other token **in parallel**.

> [!gap] Thin sourcing
> None of the four ingested repos has a detailed Transformer note: the AI-Notes `Transformers.md` and `Attention Model.md` are empty stubs, the DLAI summary (2018) predates Transformers, and Denny Britz's list links the paper without a note. This page assembles what the sources do cover. Ingest *The Illustrated Transformer* or the paper itself to deepen it.

## Why it replaced RNNs (from [[Large Language Models]])

LSTM encoder-decoders with attention process tokens **one at a time**, so they don't parallelize and are slow on long text. The Transformer keeps attention and drops the LSTM.

## Ingredients already in this wiki

| Component | Origin in the sources |
|-----------|-----------------------|
| Scaled **dot-product** attention | Luong's dot score in [[Effective Approaches to Attention-Based Neural Machine Translation]]; Bahdanau attention in [[Attention Mechanism]] |
| **Multi-head** attention | Multi-row attention in [[A Structured Self-Attentive Sentence Embedding]] |
| Query, key, value memory reads | [[End-To-End Memory Networks]], [[Neural Turing Machines]] |
| Residual connections | [[Residual Networks]] |
| Layer normalization | [[Layer Normalization]] |
| Warmup, then inverse-square-root LR schedule | [[Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer]] |
| Subword tokens | [[Neural Machine Translation of Rare Words with Subword Units]] |
| Linear-time CNN alternative of the same era | [[Neural Machine Translation in Linear Time]] |

## Block structure (standard description)

Each layer: multi-head self-attention, then add and layer-norm, then a position-wise feed-forward network, then add and layer-norm. Positional encodings are added to the embeddings because attention itself is order-blind. The decoder uses **masked** (causal) self-attention plus cross-attention over the encoder outputs.

Families: encoder-only (BERT, using MLM), decoder-only (GPT, using CLM), encoder-decoder (T5).
