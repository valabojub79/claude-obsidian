---
type: concept
title: "End-to-End Deep Learning"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - ml-strategy
complexity: intermediate
domain: deep-learning
status: developing
address: c-000150
related:
  - "[[DLAI Course 3 - Structuring Machine Learning Projects]]"
  - "[[Face Recognition]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/3- Structuring Machine Learning Projects/Readme.md]]"
---

# End-to-End Deep Learning

Replace a multi-stage pipeline with one network mapping input directly to output.

| Task | Pipeline | End-to-end | Winner (2017) |
|------|----------|-----------|---------------|
| Speech recognition | audio, features, phonemes, words, transcript | audio to transcript | End-to-end, with large data |
| Face-gated turnstile | detect face, crop, then compare identities | raw camera image to identity | **Two-step**: lots of data exists for each sub-task |
| Machine translation | text analysis ... French | English to French | End-to-end (lots of paired data) |
| Child's age from hand X-ray | segment bones, lengths, age table | image to age | **Pipeline** (too little data) |

## Pros

- Lets the data speak: no forced human concepts such as phonemes.
- Less hand-engineering.

## Cons

- Needs a lot of (x, y) data.
- Throws away useful hand-designed components, which matter most when data is small.

## Key question

Do you have enough data to learn a function of the **complexity** needed to map x to y? If not, break the problem into sub-tasks you *can* get data for. Each step can still be a neural network (as in [[Face Recognition]]).
