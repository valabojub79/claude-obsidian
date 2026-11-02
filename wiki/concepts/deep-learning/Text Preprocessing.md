---
type: concept
title: "Text Preprocessing"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - preprocessing
complexity: beginner
domain: deep-learning
status: developing
address: c-000197
related:
  - "[[Word Embeddings]]"
  - "[[Language Models and Sequence Generation]]"
sources:
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/Text Cleaning.md]]"
---

# Text Preprocessing

Cleaning raw text before building embeddings or features. From [[ai-notes|AI-Notes]]. Text cleaning "is an art": the steps depend on the data.

## Data sources

Public datasets, web scraping, APIs, internal databases. Scraped and social data is the dirtiest.

## Common pipeline

1. **Tokenization**: sentence level, word level, or character level (NLTK `sent_tokenize`, `word_tokenize`).
2. **Lowercasing**: merges `Hut` and `hut` and shrinks the vocabulary. Caveat: `US` (the country) becomes `us`.
3. **HTML tag removal** (scraped text).
4. **Emoji and special-character handling**: on social media, *encode* emojis (they carry sentiment) rather than delete them.
5. **Stop-word removal** ("is", "a", "the"): shrinks the vocabulary; skip it for tasks where function words matter (negation in sentiment).
6. **Punctuation removal**.
7. **Stemming or lemmatization**: reduce inflections to a base form.

## Stemming vs lemmatization

| | Stemming | Lemmatization |
|-|----------|---------------|
| Method | Rule-based suffix and prefix stripping | POS tagging plus dictionary lookup |
| Output | May not be a real word ("studi") | Always a valid lemma ("study") |
| Cost | Cheap | Slower |

Stemmers: **Porter** (simple suffix rules), **Regexp** (custom patterns), **Snowball** (refined Porter, multilingual).

Failure modes: **over-stemming** (universal, university and universe collapse to "univers") and **under-stemming** (related forms left separate).

## Modern note

Subword tokenizers (BPE, WordPiece; see [[Neural Machine Translation of Rare Words with Subword Units]]) and pretrained Transformers make most of these steps unnecessary or harmful. Lowercasing, stemming and stop-word removal throw away signal those models use. They remain useful for bag-of-words, TF-IDF and classical ML.
