---
type: concept
title: "RAG Architecture"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - rag
complexity: intermediate
domain: generative-ai
status: developing
address: c-000337
related:
  - "[[Chunking Techniques]]"
  - "[[Hybrid Search]]"
  - "[[LLM and RAG Evaluation]]"
  - "[[Fine-Tuning LLMs]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/RAG Systems/Basic RAG/RAG Architecture.md]]"
---

# RAG Architecture

**Retrieval-Augmented Generation**: answer questions over private or specialized data **without fine-tuning** the LLM, by retrieving relevant context and passing it alongside the query. From [[ai-notes|AI-Notes]].

## Four components

1. **Text splitter**: split documents into chunks. The context window is limited, and only parts are relevant anyway. See [[Chunking Techniques]].
2. **Embedder**: embed chunks and store them in a **vector database**.
3. **Retriever**: given the query, fetch the most relevant chunks (vector, keyword or [[Hybrid Search|hybrid]] search; optionally re-rank).
4. **Generator**: the LLM answers using query plus retrieved context.

```
docs -> split -> embed -> vector DB
query -> embed -> retrieve top-k -> [re-rank] -> prompt(query + context) -> LLM -> answer
```

## Advanced RAG (AI-Notes sections)

- Better chunks: [[Chunking Techniques]] (semantic and agentic).
- Better retrieval: [[Hybrid Search]] (BM25 plus dense vectors).
- Re-ranking (cross-encoder rescoring of the top-k): the source page is a stub.
- Evaluation: RAGAS in [[LLM and RAG Evaluation]].

## RAG vs fine-tuning

RAG injects **knowledge** at query time (updatable, citable); fine-tuning changes **behavior or style** ([[Fine-Tuning LLMs]]). They combine well.

Concept lineage: memory-augmented networks such as [[End-To-End Memory Networks]] attended over stored sentences, a learned, small-scale ancestor of retrieve-then-read. See also [[Large Language Models]].
