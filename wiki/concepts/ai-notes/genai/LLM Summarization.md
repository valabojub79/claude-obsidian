---
type: concept
title: "LLM Summarization"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - summarization
complexity: beginner
domain: generative-ai
status: developing
address: c-000333
related:
  - "[[Large Language Models]]"
  - "[[A Neural Attention Model for Abstractive Sentence Summarization]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/LLM Summarization/LLM for Summarization.md]]"
---

# LLM Summarization

From [[ai-notes|AI-Notes]] (Arize blog; long-document summarization survey arXiv 2207.00939; "5 levels of summarization" video).

**Why:** efficient storage and retrieval, and better retention because redundancy is removed. **Uses:** pulling core concepts across many documents, meeting summaries (Zoom AI), product-review summaries (Amazon).

## Approaches

| | Extractive | Abstractive |
|-|-----------|-------------|
| What | Select and concatenate source sentences | Generate new text that captures the meaning |
| Pro | High factual fidelity | Fluent, human-like |
| Con | Choppy; ignores coherence between sentences | Can hallucinate or introduce bias |

**Hybrid:** extract the key content first, then have an LLM rewrite and refine it. Common for documents longer than the context window, alongside map-reduce and refine chains. Count tokens first (OpenAI tokenizer tool) to choose a strategy.

## History in the paper notes

Neural abstractive summarization began with attention seq2seq for headlines ([[A Neural Attention Model for Abstractive Sentence Summarization]]) and copy mechanisms ([[Incorporating Copying Mechanism in Sequence-to-Sequence Learning]]), and was evaluated with ROUGE.
