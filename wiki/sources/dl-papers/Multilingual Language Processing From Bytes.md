---
type: source
title: "Multilingual Language Processing From Bytes"
source_type: paper
year: 2015
url: "http://arxiv.org/abs/1512.00103"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nlp
  - multilingual
  - character-level
  - ner
status: ingested
address: c-000263
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Sequence to Sequence Models]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/multilingual-language-processing-from-bytes.md]]"
---

# Multilingual Language Processing From Bytes

[Paper](http://arxiv.org/abs/1512.00103) (2015) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Gillick et al.'s **Byte-to-Span (BTS)**: a seq2seq LSTM reads **raw UTF-8 bytes** from many languages (examples shuffled together) and outputs spans as `[start, length, label]` tokens for POS tagging and NER. State of the art or close, with **one compact model (about 1M parameters)** for all languages.

## Data and results

POS: 13 languages, average 95.85% (vs CRF 95.41). NER F1 en/de/es/nl: 86.50 / 76.22 / 82.95 / 82.84.

## Key points

- 4 LSTM layers of 320 units, 320-d embeddings, dropout 0.2 to 0.3. Only 256 input symbols, so the model is tiny.
- **Byte dropout** (replace inputs with a `DROP` symbol) plus dropout lifts NER F1 from 74 to 78 to 82.
- Input split into 60-byte segments with 50% overlap. Low-resource languages gain most from multilingual training.
- Recall is hard to tune because non-spans aren't annotated.

## Critique (Denny Britz)

Is the fixed-vector encoding a bottleneck (why not attention, longer `k`)? Is LSTM state kept across segments? Why not a BiLSTM? What are the "shared high-level representations"? How do you add a new language?
