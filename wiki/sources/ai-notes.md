---
type: source
title: "AI-Notes"
source_type: repository
author: "Yuvraj Singh (yuvraaj2002)"
date_published: 2024-08-01
date_ingested: 2026-11-02
created: 2026-11-02
updated: 2026-11-02
url: "https://github.com/yuvraaj2002/AI-Notes"
commit: 822359aeea08fbe3c4f6861510059df3e7908ea7
license: "none stated"
confidence: medium
tags:
  - source
  - machine-learning
  - deep-learning
  - interview-prep
status: ingested
address: c-000128
related:
  - "[[AI-Notes Study Roadmap]]"
  - "[[Deep Learning]]"
  - "[[Large Language Models]]"
  - "[[Data Structures and Algorithms]]"
sources:
  - ".raw/repos/AI-Notes/"
key_claims:
  - "Interview-oriented Q&A notes spanning ML, DL, GenAI/RAG, statistics, Python, SQL/DBMS, DSA and system design"
  - "Mostly based on CampusX videos, Krish Naik, Love Babbar and Hands-On ML"
  - "Contains several factual slips, corrected and flagged in the wiki pages"
---

# AI-Notes (yuvraaj2002)

An Obsidian vault of **interview-preparation notes** by an AI/ML student: 213 Markdown notes plus images, notebooks and PDFs (828 MB in total). Mostly Q&A style ("What is X? Drawbacks? How is it solved?"), based on CampusX, Krish Naik, Love Babbar, Arpit Bhayani and *Hands-On Machine Learning*. **No license is stated**; the wiki paraphrases and attributes. A text-only snapshot at `822359a` is stored locally (gitignored) in `.raw/repos/AI-Notes/` (images, PDFs and notebooks excluded).

## How it was integrated

- **201 notes** outside `Tags/` (the 12 tag pages are just link hubs): **144** have content and **57** are empty or under 100 bytes (listed below).
- **Overlapping deep-learning notes were merged** into the existing DLAI and LISA pages as "AI-Notes perspective" sections (ANN, activations, BatchNorm, dropout, weight init, optimizers, RNN, LSTM, GRU, encoder-decoder, word embeddings, CNN, logistic regression, gradient descent, object detection), not duplicated.
- Everything else got its own page under `wiki/concepts/ai-notes/` (101 pages), with tiny sibling files merged (the 9 behavioral-question lists, the string sub-notes, the two MLOps notes, the tree notes).
- **Errors in the source** are corrected inline and flagged with `[!contradiction]` callouts, for example: test-time vs inverted dropout, the GRU date, Sobel/Scharr orientation, word2vec embedding weights, the t-test sample-size rule, Pareto alpha, chi-square critical value vs p-value, confidence level vs beta, the F-statistic orientation, the R^2 range and formula, and "function overloading" in Python.

## Sections and wiki pages

| AI-Notes folder | Wiki location | Hub |
|-----------------|---------------|-----|
| Deep Learning | merged into `concepts/deep-learning/`, plus [[Text Preprocessing]] | [[Deep Learning]] |
| Generative AI, Research Papers | `concepts/ai-notes/genai/` | [[Large Language Models]] |
| Machine Learning | `concepts/ai-notes/ml/` | [[Ensemble Learning]], [[Linear Regression]] |
| General ML Topics | `concepts/ai-notes/ml-practice/` | [[Bias Variance Tradeoff]] |
| Unsupervised Learning | `concepts/ai-notes/unsupervised/` | [[Clustering Algorithms]] |
| Mathematics | `concepts/ai-notes/math-stats/` | [[Probability Distributions]], [[Hypothesis Testing]] |
| Python | `concepts/ai-notes/python/` | [[Object-Oriented Programming in Python]] |
| Database Management System | `concepts/ai-notes/databases/` | [[Database Fundamentals]], [[SQL Overview]] |
| Data Structures and Algorithms | `concepts/ai-notes/dsa/` | [[Data Structures and Algorithms]] |
| System Design | `concepts/ai-notes/system-design/` | [[Client-Server Architecture]] |
| MLOPS | `concepts/ai-notes/career/` | [[MLOps Data Management and Versioning]] |
| Behavioral Questions, Preparation Index, Things To Learn | `concepts/ai-notes/career/` | [[AI-Notes Study Roadmap]], [[Behavioral Interview Questions]] |

> [!gap] 57 empty or stub notes in the source
> **DSA**: Heap, Recursion-DP, Stack-Queue, Stack conversion and implementation, String/Searching and Indexing. **DBMS**: 4 case-study solutions (Data Science Jobs, Google Play, Indian Tourism, Swiggy), Data Models, ER Model, Indexing, Case Studies, and 11 SQL pages (aggregates, clauses, CTE, constraints, datatypes, filtering, stored procedures, built-ins, operators, order of execution, commands). **DL**: Transfer Learning, Attention Model, Transformers, Images/Untitled. **ML**: Feature Extraction. **GenAI**: Re-Ranking. **MLOps**: 11 of 13 pages. **Math**: Loss functions, MLE, Transformations, Binomial, Normal, Empirical Rule, Measure of Dispersion, Types of Sampling. **Python**: Dictionary, List, Set, Tuple, Exception Handling. **Unsupervised**: Density-Based Clustering, Autoencoders.
>
> Where other pages link to these topics, the wiki fills in a standard explanation and marks it with a gap callout (for example [[Transformer Architecture]], [[Maximum Likelihood Estimation]], [[Empirical Rule]], [[Transformations]], [[Microservices Architecture]]).

## Reliability

Good coverage of breadth and typical interview angles; uneven depth; several unfinished sections ("Remaining questions" checklists). Treat it as a study guide, and prefer the DLAI and LISA pages and the paper notes for deep-learning detail.
