---
type: concept
title: "Sequence to Sequence Models"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - sequence-models
complexity: advanced
domain: deep-learning
status: developing
address: c-000193
related:
  - "[[Attention Mechanism]]"
  - "[[Beam Search]]"
  - "[[Recurrent Neural Networks]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/Encoder Decoder.md]]"
---

# Sequence to Sequence Models

## Encoder-decoder

- **Encoder** RNN (LSTM or GRU) reads the input sequence into a vector.
- **Decoder** RNN generates the output sequence from that vector.

Sutskever et al. 2014; Cho et al. 2014. Used for machine translation and speech.

**Image captioning** uses the same pattern with a pretrained CNN (AlexNet) as encoder and an RNN decoder (Mao 2014; Vinyals "Show and Tell" 2014; Karpathy and Fei-Fei 2015).

## "Conditional language model"

The decoder is a [[Language Models and Sequence Generation|language model]] whose initial state is the encoding instead of zeros:

```
LM:  P(y<1..Ty>)
MT:  P(y<1..Ty> | x<1..Tx>)
```

For translation we want the **most likely** output, not a random sample:

```
argmax_y P(y<1>, ..., y<Ty> | x)
```

## Why not greedy?

Picking the top word each step fails. After "Jane is", "going" is more common than "visiting", leading to the worse "Jane is going to be visiting Africa...". The joint probability needs a search: [[Beam Search]].

## Limits

Squeezing a long sentence into one fixed vector hurts; BLEU drops for sentences beyond about 20 words. [[Attention Mechanism]] fixes this.

## Evaluation

[[BLEU Score]].

## AI-Notes perspective

[[ai-notes|AI-Notes]]' long interview-style page (based on Jay Alammar's illustrated posts and the Sutskever paper):

- **Seq2seq vs encoder-decoder**: seq2seq names the task family (sequence in, sequence out, lengths may differ); encoder-decoder is the more general architecture (also used for images to captions and the like). Sequence *modeling* can be one-to-many or many-to-many; seq2seq is always many-to-many.
- **Components**: encoder (LSTM or GRU over embeddings), **context vector** (final hidden and cell states; its size is the encoder's hidden units, typically 256 to 1024), decoder.
- **Training**: add `<START>` and `<END>` tokens; the decoder predicts a softmax per step while the true previous token is fed in (**teacher forcing**).
- **Inference**: start with `<START>` and feed each prediction back in, so early mistakes propagate. This is the exposure-bias problem tackled by [[Professor Forcing - A New Algorithm for Training Recurrent Networks]].
- **Limitation**: the fixed-size context vector bottleneck. The fixes are a **bidirectional encoder** and **attention** (pass *all* encoder states; at each decoder step score them, softmax, and take the weighted sum). See [[Attention Mechanism]].
- Suggested reading order: Alammar's attention post, then *The Illustrated Transformer*, then *The Illustrated BERT*.
