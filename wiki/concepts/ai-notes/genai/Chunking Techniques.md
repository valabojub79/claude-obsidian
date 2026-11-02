---
type: concept
title: "Chunking Techniques"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - rag
complexity: intermediate
domain: generative-ai
status: developing
address: c-000328
related:
  - "[[RAG Architecture]]"
  - "[[LangChain]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/RAG Systems/Advance RAG/Chunking Techniques.md]]"
---

# Chunking Techniques

How you split documents largely determines RAG quality: if a chunk doesn't contain the answer, or splits it in half, the LLM answers incompletely or wrongly. From [[ai-notes|AI-Notes]] (Greg Kamradt's "5 Levels of Text Splitting", mer.vin code).

## The five levels

1. **Character splitting**: fixed-size chunks with `chunk_overlap` for some continuity. Simple, but cuts words and ideas mid-way.

   ```python
   from langchain.text_splitter import CharacterTextSplitter
   splitter = CharacterTextSplitter(chunk_size=35, chunk_overlap=10, separator='')
   ```

2. **Recursive character splitting**: tries a hierarchy of separators (paragraphs, sentences, words) so chunks stay within `chunk_size` without breaking words. The usual default.
3. **Document-specific splitting**: respect structure (Markdown headers, code functions and classes, PDF tables).
4. **Semantic (embedding) splitting**: embed sentences and cut where the similarity between neighbors drops, so each chunk is one topic.
5. **Agentic splitting**: an LLM decides chunk boundaries and propositions. The notes rate it best quality, at the highest cost.

Evaluate chunking choices with RAGAS ([[LLM and RAG Evaluation]]).

> [!gap] Unfinished in source
> The semantic-chunking section is a heading plus links.
