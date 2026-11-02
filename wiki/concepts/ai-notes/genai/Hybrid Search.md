---
type: concept
title: "Hybrid Search"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - rag
  - information-retrieval
complexity: intermediate
domain: generative-ai
status: developing
address: c-000330
related:
  - "[[RAG Architecture]]"
  - "[[Word Embeddings]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/RAG Systems/Advance RAG/Hybrid Search.md]]"
---

# Hybrid Search

```
hybrid = dense vector search (semantic) + sparse keyword search (lexical)
```

From [[ai-notes|AI-Notes]] (Weaviate's hybrid search and fusion-algorithm posts; BM25 and SBERT videos).

## Why add keywords to vectors?

Dense (semantic) search matches **meaning** but can miss exact terms: product codes, names, rare jargon. Keyword search matches **exact terms**. Combined, retrieval captures both nuance and precision, which feeds the LLM better context ([[RAG Architecture]]).

## Where the vectors come from

- **Sparse**: TF-IDF, **BM25** (TF-IDF with term-frequency saturation and length normalization), **SPLADE** (learned sparse). See TF-IDF in [[Word Embeddings]].
- **Dense**: GloVe-style or **Transformer sentence embeddings** (SBERT and the like).

## Fusing the result lists

Typical methods (from the linked Weaviate posts): **Reciprocal Rank Fusion** (sum of `1/(k + rank)`) or relative-score fusion with a weight `alpha` between keyword and vector scores.

Related: **self-query retrieval** (an LLM turns the question into metadata filters plus a semantic query).
