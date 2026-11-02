---
type: concept
title: "Fine-Tuning LLMs"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - fine-tuning
complexity: intermediate
domain: generative-ai
status: developing
address: c-000329
related:
  - "[[Large Language Models]]"
  - "[[LLM Quantization]]"
  - "[[Transfer Learning]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/Finetuning and Quantization/Fine Tuning LLM.md]]"
---

# Fine-Tuning LLMs

From [[ai-notes|AI-Notes]] (Krish Naik and other crash courses, plus EleutherAI's *Transformer Math 101*).

## Three ways to get a capable model

1. **Pretraining**: terabytes of text, a chosen architecture, and a tokenizer (text to token IDs plus special tokens). Objective: next-token prediction (causal) or masked-token filling. The result knows language in general but no specific task. See [[Large Language Models]].
2. **Full fine-tuning**: continue training on task data. **Instruction tuning** uses instruction-response pairs (Q&A and similar) to optimize a task loss.
3. **Parameter-efficient fine-tuning**: **LoRA and QLoRA**.

## LoRA and QLoRA

- Full fine-tuning is expensive: all weights plus optimizer states.
- **LoRA** (low-rank adaptation) freezes the base weights and learns small low-rank update matrices, so far fewer trainable parameters and much less optimizer memory.
- **QLoRA** loads the base model **quantized** (4-bit, via `bitsandbytes`) and trains LoRA adapters on top. See [[LLM Quantization]].
- The notes' rough hardware estimate for a 7B model (Llama-2 7B, Mistral 7B): full fine-tuning about 150 to 195 GB (on the order of 16 A100s of 80 GB, by the source's estimate); QLoRA on **2 RTX 3090s or 1 A100**.
- GPU rental: RunPod (rated best), Vast.ai (cheapest), Lambda Labs, AWS SageMaker, Google Colab.
- A rule of thumb in the notes: a fine-tuning dataset of about 10 MB is a sensible starting size.

## The reversal curse and data augmentation

LLMs trained on "A is B" often fail on "B is A". Mitigation: present facts **from multiple angles**. Have an LLM rephrase each statement or Q&A pair in several ways, at different temperatures, before fine-tuning.

## Before you fine-tune

Benchmark the base model, and a [[RAG Architecture|RAG]] setup, first. Many "knowledge" needs are better served by retrieval than by changing weights.

> [!gap] Unfinished in source
> The source's "need for fine-tuning", "techniques" and hyperparameter sections are empty headings.
