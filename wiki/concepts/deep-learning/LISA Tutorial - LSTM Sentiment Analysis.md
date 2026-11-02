---
type: concept
title: "LISA Tutorial - LSTM Sentiment Analysis"
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
address: c-000170
related:
  - "[[Long Short-Term Memory]]"
  - "[[Word Embeddings]]"
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/lstm.txt]]"
---

# LISA Tutorial: LSTM Networks for Sentiment Analysis

Binary sentiment (positive or negative) on the IMDB Large Movie Review Dataset (Maas et al. 2011), in Theano. Authors: Pierre Luc Carrier and Kyunghyun Cho.

## Motivation, in eigenvalue terms

In a plain RNN, backprop multiplies the gradient by the recurrent matrix once per time step. If its **leading eigenvalue is below 1**, gradients **vanish**; above 1, they **explode** (see [[Vanishing and Exploding Gradients]]). LSTM's **memory cell** has a self-connection of weight 1.0, so its state persists unless the gates intervene.

## Equations (as in the tutorial)

```
i_t  = sigma(W_i x_t + U_i h_{t-1} + b_i)                 # input gate
C~_t = tanh (W_c x_t + U_c h_{t-1} + b_c)                 # candidate
f_t  = sigma(W_f x_t + U_f h_{t-1} + b_f)                 # forget gate
C_t  = i_t * C~_t + f_t * C_{t-1}
o_t  = sigma(W_o x_t + U_o h_{t-1} + b_o)                 # variant: no V_o C_t peephole
h_t  = o_t * tanh(C_t)
```

Compare DLAI's notation in [[Long Short-Term Memory]].

**Implementation trick:** stack `W_i, W_f, W_c, W_o` into one matrix (and the same for `U` and `b`), compute `z = W x_t + U h_{t-1} + b` once, then slice. Four matrix products become one.

## Architecture

Embeddings, one LSTM layer, **mean pooling over time** of all `h_t`, then logistic regression.

## Training tips

- Use **AdaDelta or RMSProp**: plain SGD "appears to perform poorly" here (see [[Optimization Algorithms]]).
- `imdb_preprocess.py` tokenizes custom data; `imdb.dict.pkl.gz` maps words to indices.

## Key papers

Hochreiter & Schmidhuber 1997 (LSTM); Gers et al. 2000 (forget gate); Graves 2012 (sequence labelling); Bengio et al. 1994 (long-term dependencies are hard).
