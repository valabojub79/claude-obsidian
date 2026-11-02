---
type: concept
title: "LLM and RAG Evaluation"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - generative-ai
  - generative-ai
  - llm
  - evaluation
  - bias
complexity: intermediate
domain: generative-ai
status: developing
address: c-000334
related:
  - "[[RAG Architecture]]"
  - "[[BLEU Score]]"
  - "[[Word Embeddings]]"
sources:
  - "[[.raw/repos/AI-Notes/Generative AI/LLM and RAG Evaluation/Evaluating LLM and RAG.md]]"
---

# LLM and RAG Evaluation

From [[ai-notes|AI-Notes]]: two notes, *Evaluating LLM and RAG* (RAGAS-focused) and *Evaluating Gender Bias and Demographic Diversity*.

## What an evaluation framework should cover

Quantitative and qualitative metrics; model size and complexity; training-data quality and diversity; **bias and fairness**; ethics and responsible use; fine-tuning and transfer effects; explainability and traceability; **robustness to adversarial attacks**; continuous monitoring.

## Metric families

| Family | Examples |
|--------|----------|
| Word or character overlap | **BLEU** ([[BLEU Score]]), **ROUGE**, WER |
| Embedding-based | BERTScore, MoverScore, WEAT |
| Language-model-based | NLI score, BLEURT, QA-QG score |
| LLM-assisted (LLM as judge) | **RAGAS**, Arize, GPTScore, G-Eval |

**RAGAS** scores RAG pipelines on retrieval and generation quality (faithfulness to the context, answer relevance, context precision and recall). See [[RAG Architecture]].

## Gender bias evaluation

LLM apps are used worldwide, so biased outputs scale harm. Three common methods:

1. **WEAT** (Word Embedding Association Test): measures association strength between target words (male/female names) and attribute words (career/family) in embedding space. Related to debiasing in [[Word Embeddings]].
2. **Direct probing**: prompts that require gender-related decisions, then analysis of the outputs.
3. **Benchmark datasets** such as **Winogender** schemas (coreference with occupations).

Paper notes (arXiv 2308.14921, *Gender bias and stereotypes in LLMs*): even after RLHF, LLMs **use gender stereotypes**, and when asked to explain they **rationalize** or claim the stereotype is true, reflecting their training data.
