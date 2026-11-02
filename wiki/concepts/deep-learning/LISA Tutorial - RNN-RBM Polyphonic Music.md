---
type: concept
title: "LISA Tutorial - RNN-RBM Polyphonic Music"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - lisa-tutorial
  - theano
  - generative
  - rnn
complexity: advanced
domain: deep-learning
status: developing
address: c-000174
related:
  - "[[LISA Tutorial - Restricted Boltzmann Machines]]"
  - "[[Recurrent Neural Networks]]"
  - "[[Energy-Based Models]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/rnnrbm.txt]]"
---

# LISA Tutorial: RNN-RBM for Polyphonic Music

Boulanger-Lewandowski, Bengio, Vincent (ICML 2012). Generate **polyphonic** music, where several notes sound at once. The per-time-step distribution over 88 piano keys is high-dimensional and **multimodal**, which a softmax or independent sigmoids can't capture.

## Model

At each time step `t`, an [[LISA Tutorial - Restricted Boltzmann Machines|RBM]] models the frame `v(t)` (a binary piano-roll vector), with biases set by an RNN summarizing the history:

```
b_v(t) = b_v + W_uv u(t-1)
b_h(t) = b_h + W_uh u(t-1)
u(t)   = tanh(b_u + W_uu u(t-1) + W_vu v(t))
P({v(t)}) = prod_t P(v(t) | history)        # (the tutorial writes it as a sum of log terms)
```

## Training and generation

- **Training**: given the sequence, all `u(t)` and therefore all RBM biases are deterministic. Run CD on every time step's RBM in one batch, and backprop the CD gradient into the RNN parameters through the biases.
- **Generation**: sample sequentially. At each step run a Gibbs chain for `v(t)`, then feed it into the RNN.

Implemented with `build_rbm` (Gibbs chain via CD; batch or single frame) and `build_rnnrbm` (recurrence serving both modes). Python 2 only.

## Results

Nottingham folk-tune dataset, 200 epochs, about 24 h. Outputs are piano rolls plus MIDI files.

## Suggested improvements

- **Preprocessing**: transpose to a common key (C major or minor) and normalize tempo. This has the biggest effect.
- **Pretraining**: independent RBMs on shuffled frames (recurrent weights 0), then the RNN.
- **Optimization**: gradient clipping, Nesterov momentum, NADE instead of RBM for the conditional density.
- Tune RBM and RNN learning rates separately; learn `u(0)`.

## Related

Later music models: LSTM (Magenta), Transformer (Music Transformer), diffusion.
