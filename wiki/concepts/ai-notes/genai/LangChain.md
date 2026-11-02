---
type: concept
title: "LangChain"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - tooling
complexity: beginner
domain: generative-ai
status: developing
address: c-000335
related:
  - "[[RAG Architecture]]"
  - "[[LLM Agents]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/Langchain.md]]"
---

# LangChain

From [[ai-notes|AI-Notes]]: a Python framework for composing LLM applications (prompts, models, parsers, retrievers, memory).

## LCEL: LangChain Expression Language

Chain **runnables** with the pipe operator; the result is itself a runnable (`invoke`, `stream`, `batch`, or chain it further):

```python
chain = prompt | llm | parser
chain.invoke({"question": "..."})
```

## Chat memory

`RunnableWithMessageHistory` wraps a runnable and reads and updates the conversation history for it.

## Where it's used in these notes

Text splitters for [[Chunking Techniques]] (`CharacterTextSplitter`, `RecursiveCharacterTextSplitter`); retrieval chains for [[RAG Architecture]]. Alternatives for agents: LangGraph, CrewAI, AutoGen (see [[LLM Agents]]).

> [!gap] Stub
> The source's "different LangChain components" section is an empty heading.
