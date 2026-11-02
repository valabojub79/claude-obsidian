---
type: concept
title: "LISA Tutorial - RNN for Slot Filling"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - nlp
  - rnn
complexity: intermediate
domain: deep-learning
status: developing
address: c-000173
related:
  - "[[Recurrent Neural Networks]]"
  - "[[Word Embeddings]]"
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/rnnslu.txt]]"
---

# LISA Tutorial: RNNs with Word Embeddings for Slot Filling

Mesnil, He, Deng, Bengio (Interspeech 2013). Spoken language understanding: label every word in an utterance with a **slot**.

## Task: ATIS

| show | flights | from | Boston | to | New | York | today |
|------|---------|------|--------|----|-----|------|-------|
| O | O | O | B-dept | O | B-arr | I-arr | B-date |

- **IOB** tagging (Inside, Outside, Beginning). 128 classes including `O`.
- 4,978 train and 893 test sentences, average length 15 words. Split train 80/20 for validation.
- Preprocessing: words seen once become `<UNK>`; digits become `DIGIT` (`1984` becomes `DIGITDIGITDIGITDIGIT`).
- Small data: an F1 difference must exceed **0.6%** to be significant at 95%. Evaluate with the `conlleval` script; a chunk is correct only if B, I and O are all right.

## Model: Elman RNN with context windows

1. **Context window**: each word becomes the indices of the `d` surrounding words (padding `-1` at the edges), say `d = 7`.
2. **Embedding lookup**: indices map to vectors, concatenated, giving a `(sentence_length, emb_dim * d)` matrix.
3. **Elman RNN** via `theano.scan`: `h_t = sigmoid(W_x x_t + W_h h_{t-1} + b)`, then softmax over slots.

Learned: embeddings, initial hidden state `h0`, `W_x`, `W_h`, the output layer (bias optional; the authors recommend skipping it).

## Training

- One SGD update per **sentence** (sentence = minibatch).
- **Normalize embeddings onto the unit sphere** after each update.
- Early stopping on validation F1, keeping the best epoch.
- **Random search** (KISS): lr `U[0.01, 0.05]`, window `{3..19}`, hidden units `{100, 200}`, embedding dim `{50, 100}`.

## Result

**94.48% F1** after a few epochs (under 40 s per epoch on an i7, under 200 MB RAM). Embedding neighbors are partly sensible (atlanta: phoenix, denver, tacoma...), partly not, given the roughly 500-word vocabulary.

Concepts: [[Recurrent Neural Networks]], [[Word Embeddings]]. Modern equivalent: BiLSTM-CRF, then BERT token classification.
