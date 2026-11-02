---
type: source
title: "Neural Machine Translation in Linear Time"
source_type: paper
year: 2016
url: "https://arxiv.org/abs/1610.10099"
note_author: "Denny Britz"
created: 2026-11-02
updated: 2026-11-02
tags:
  - source
  - paper
  - deep-learning
  - nmt
  - cnn
  - character-level
status: ingested
address: c-000266
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Fully Character-Level Neural Machine Translation without Explicit Segmentation]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/notes/nmt-linear-time.md]]"
---

# Neural Machine Translation in Linear Time

[Paper](https://arxiv.org/abs/1610.10099) (2016) | Notes by Denny Britz | Index: [[deeplearning-papernotes|Deep Learning Paper Notes]]

**TL;DR:** Kalchbrenner et al.'s **ByteNet**: a WaveNet-style architecture for translation. A dilated-CNN **source network** with a dilated, **masked** (causal) CNN **target network** stacked on top. Runtime is `O(|S| + |T|)`, versus `O(|S| x |T|)` for attention seq2seq.

## Properties

- **Resolution preserving**: the source representation grows with source length (no fixed vector).
- Source encoding is parallel; **dilation** grows the receptive field exponentially, so paths between tokens are short and backprop is easy.
- **Dynamic unfolding**: source representation at step `t` feeds target step `t` (zero-padded beyond the source length).
- Residual blocks (ReLU or multiplicative units); **sub-batch normalization** to avoid leaking future tokens.

## Results

- Hutter Prize character LM: new state of the art, **1.33 bits/char**.
- Character-level WMT EN-DE: **18.9 BLEU** (attention enc-dec 20.6; state of the art about 22.8). Uses bags of character n-grams as extra embeddings.

## Critique (Denny Britz)

Close to WaveNet plus PixelCNN, with no equations or code, so hard to reproduce. Where are wall-clock speedups in practice? Dynamic unfolding suits well-aligned language pairs but may hurt poorly aligned ones (attention always has path length 1). How much do the n-gram embeddings contribute?
