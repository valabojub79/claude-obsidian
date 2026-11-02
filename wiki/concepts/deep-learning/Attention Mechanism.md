---
type: concept
title: "Attention Mechanism"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - nlp
  - sequence-models
  - attention
complexity: advanced
domain: deep-learning
status: developing
address: c-000130
related:
  - "[[Sequence to Sequence Models]]"
  - "[[Transformer Architecture]]"
  - "[[Neural Machine Translation by Jointly Learning to Align and Translate]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
---

# Attention Mechanism

Bahdanau, Cho, Bengio, 2014: *Neural Machine Translation by Jointly Learning to Align and Translate*. Ng calls it one of the most influential ideas in deep learning.

## Motivation

A human translator doesn't memorize a whole paragraph and then write; they look back at the relevant part. Plain [[Sequence to Sequence Models|encoder-decoders]] lose BLEU on long sentences; attention keeps BLEU flat as length grows.

## Model

1. **Encoder**: a bidirectional RNN (usually LSTM) gives annotations `a<t'> = [a_fwd<t'>; a_bwd<t'>]` for each input position `t'`.
2. **Decoder**: a unidirectional RNN with state `s<t>`. At each output step `t` it receives a **context vector**:

```
c<t>         = sum_{t'} alpha<t,t'> a<t'>
alpha<t,t'>  = exp(e<t,t'>) / sum_{t''} exp(e<t,t''>)      # softmax over input positions
e<t,t'>      = small_NN( s<t-1>, a<t'> )                    # 1-hidden-layer "alignment" net
```

`alpha<t,t'>` is how much output `t` attends to input `t'`; for each `t` the weights sum to 1. The alignment network is trained jointly by backprop.

## Cost and insight

- Cost is `Tx * Ty` (quadratic), acceptable for sentences.
- **Visualizing `alpha`** gives a soft word-alignment matrix, close to the diagonal for similar word order.

## Keras assignment (date normalization)

"Pre-attention" BiLSTM over the input; at each output step, `RepeatVector` copies `s<t-1>` Tx times, concatenates it with `a`, passes it through Dense layers and softmax over time to get `alpha`, then takes the dot with `a` to get the context. A "post-attention" LSTM produces the output.

## Beyond RNNs

The idea grew into **self-attention** and the [[Transformer Architecture]] (Vaswani et al. 2017), dropping recurrence entirely. It is also used in vision (show, attend and tell) and neural Turing machines.

Paper page: [[Neural Machine Translation by Jointly Learning to Align and Translate]].
