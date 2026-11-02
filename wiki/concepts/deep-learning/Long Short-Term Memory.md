---
type: concept
title: "Long Short-Term Memory"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - rnn
  - sequence-models
complexity: advanced
domain: deep-learning
status: developing
address: c-000180
related:
  - "[[Gated Recurrent Unit]]"
  - "[[Recurrent Neural Networks]]"
  - "[[LISA Tutorial - LSTM Sentiment Analysis]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/LSTM.md]]"
---

# Long Short-Term Memory (LSTM)

Hochreiter & Schmidhuber, 1997. More general than the [[Gated Recurrent Unit]]: separate update and forget gates, plus an output gate, and `c<t> != a<t>`.

```
c_tilde<t> = tanh( W_c [a<t-1>, x<t>] + b_c )
Gamma_u    = sigmoid( W_u [a<t-1>, x<t>] + b_u )     # update (input) gate
Gamma_f    = sigmoid( W_f [a<t-1>, x<t>] + b_f )     # forget gate
Gamma_o    = sigmoid( W_o [a<t-1>, x<t>] + b_o )     # output gate
c<t>       = Gamma_u * c_tilde<t> + Gamma_f * c<t-1>
a<t>       = Gamma_o * tanh(c<t>)
```

Having independent `Gamma_u` and `Gamma_f` (instead of `u` and `1 - u`) lets the cell both keep old memory **and** add new. With suitable gate values, `c<0>` can flow unchanged to `c<T>`, the "constant error carousel" that defeats vanishing gradients.

## Variants

- **Peephole connections**: gates also see `c<t-1>`, element by element.
- Diagrams in Chris Olah's *Understanding LSTM Networks* are the popular visual; Ng prefers the equations.

## Usage

- The default recurrent unit through about 2017; **BiLSTM** encoders were standard in NLP.
- Keras: `LSTM(units, return_sequences=True)`.

## Related

- Theano implementation for IMDB sentiment: [[LISA Tutorial - LSTM Sentiment Analysis]].
- AI-Notes perspective: see the section below.

## AI-Notes perspective: gates in words

[[ai-notes|AI-Notes]] describes the LSTM as a **cell state** (long-term context, edited only through gates) beside the **hidden state** (short-term context, rewritten each step).

- **Input gate**: a candidate vector (new information) times a sigmoid importance vector; the product is **added** to the cell state.
- **Forget gate**: a sigmoid of `[h_{t-1}, x_t]` gives retention fractions, **multiplied** element-wise into the cell state. Example: `C = [2, 3, 4]` and `f = [0.1, 0.2, 0.5]` give `[0.2, 0.6, 2.0]`. (The source says "adding" here; it is multiplication, as its own example shows.)
- **Output gate**: decides what part of `tanh(C_t)` becomes `h_t`.

**Drawbacks:** three gates mean many parameters and slow training (motivating [[Gated Recurrent Unit|GRU]]); **unidirectional**, so no access to future context. Fix: **bidirectional LSTM** (forward and backward layers, outputs concatenated), good for sequence labeling, translation and comprehension.
