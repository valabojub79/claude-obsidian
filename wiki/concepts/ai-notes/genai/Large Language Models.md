---
type: concept
title: "Large Language Models"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
complexity: intermediate
domain: generative-ai
status: developing
address: c-000336
related:
  - "[[Transformer Architecture]]"
  - "[[Fine-Tuning LLMs]]"
  - "[[RAG Architecture]]"
  - "[[Attention Mechanism]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/History Behind LLM.md]]"
---

# Large Language Models

Notes from [[ai-notes|AI-Notes]] (CampusX lineage), connected to the deep-learning pages in this wiki.

## Lineage: RNN to Transformer

1. **RNNs** handle sequences; of the RNN shapes, **many-to-many (asynchronous)** (translation, generation) drew the most research. See [[Recurrent Neural Networks]].
2. **Encoder-decoder (seq2seq)** with LSTMs: works, but one fixed **context vector** must hold the whole input, so long inputs fail. See [[Sequence to Sequence Models]].
3. **Attention**: give the decoder *all* encoder states, with learned weights per step. Better on long text, but still sequential LSTMs plus `O(N^2)` attention, which is slow. See [[Attention Mechanism]].
4. **Transformers**: drop recurrence; "attention is all you need". Fully **parallel** over tokens gives state-of-the-art results, but they're expensive to train from scratch. See [[Transformer Architecture]].
5. **Pretrained LLMs**: train a Transformer once on huge text, then adapt (fine-tune, prompt, retrieve). Transfer learning at internet scale; see [[Transfer Learning]] and [[Unsupervised Pretraining]].

## Pretraining objectives

- **Causal language modeling (CLM)**: predict the next token (GPT family), suited to **generation**.
- **Masked language modeling (MLM)**: fill in masked tokens using both sides (BERT family), suited to understanding.

After pretraining a model knows general language but not your task or domain, hence [[Fine-Tuning LLMs]] or [[RAG Architecture|RAG]].

## Working with LLMs (AI-Notes pages)

| Need | Page |
|------|------|
| Adapt behavior or domain | [[Fine-Tuning LLMs]] (LoRA, QLoRA) |
| Run on small hardware | [[LLM Quantization]] |
| Ground answers in your data | [[RAG Architecture]], [[Chunking Techniques]], [[Hybrid Search]] |
| Measure quality and bias | [[LLM and RAG Evaluation]] |
| Summarize documents | [[LLM Summarization]] |
| Build pipelines | [[LangChain]] |
| Multi-step tool use | [[LLM Agents]] |

## Earlier steps in the wiki's paper notes

[[Exploring the Limits of Language Modeling]] (scale wins), [[Semi-Supervised Sequence Learning]] (LM pretraining, then fine-tune), [[Neural Machine Translation of Rare Words with Subword Units]] (BPE tokenization), [[Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer]] (MoE), [[Distilling the Knowledge in a Neural Network]].
