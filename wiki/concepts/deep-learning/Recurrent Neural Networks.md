---
type: concept
title: "Recurrent Neural Networks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - sequence-models
  - rnn
complexity: intermediate
domain: deep-learning
status: developing
address: c-000189
related:
  - "[[Gated Recurrent Unit]]"
  - "[[Long Short-Term Memory]]"
  - "[[Language Models and Sequence Generation]]"
  - "[[LISA Tutorial - RNN for Slot Filling]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/5- Sequence Models/Readme.md]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Text/Recurrent Neural Net.md]]"
---

# Recurrent Neural Networks

## Why not a standard network?

1. Inputs and outputs vary in length across examples; padding to the maximum is a hack.
2. A dense network shares nothing across positions. "Harry" learned at position 1 should help at position 7, the same parameter-sharing argument as for [[Convolutional Neural Networks]].

## Basic RNN cell

```
a<t>    = g( W_aa a<t-1> + W_ax x<t> + b_a )     # tanh (or ReLU)
y_hat<t> = g'( W_ya a<t> + b_y )                  # sigmoid or softmax
```

Simplified notation: `W_a = [W_aa | W_ax]` and `a<t> = g(W_a [a<t-1>; x<t>] + b_a)`. `a<0>` is usually zeros. The same weights are used at every time step.

Limitation: `y_hat<t>` sees only the past. In "He said, *Teddy* Roosevelt...", whether Teddy is a name depends on later words. The fix is a bidirectional RNN.

## Backpropagation through time (BPTT)

Loss per step is cross-entropy; total loss is the sum over `t`. Gradients flow right to left across time steps through the shared weights. Frameworks handle it, but the depth equals the sequence length, so [[Vanishing and Exploding Gradients]] are severe.

- **Exploding**: easy to spot (NaNs). Fix with **gradient clipping** (rescale when the norm exceeds a threshold) or truncated BPTT.
- **Vanishing**: subtler; the network can't carry "cat ... was" across many words. Fix with gated units ([[Gated Recurrent Unit]], [[Long Short-Term Memory]]), better init, or echo state networks.

## Architectures (after Karpathy's "Unreasonable Effectiveness of RNNs")

- **Many-to-many, Tx = Ty**: named-entity recognition.
- **Many-to-one**: sentiment analysis (read everything, predict at the end).
- **One-to-many**: music or text generation (feed each output back as the next input).
- **Many-to-many, Tx != Ty**: encoder-decoder ([[Sequence to Sequence Models]]).
- **Attention-based**: [[Attention Mechanism]].

## Bidirectional RNN (BRNN)

Run one RNN forward and one backward; predict from both: `y_hat<t> = g(W_y [a_fwd<t>; a_bwd<t>] + b_y)`. It's still an acyclic graph. **BiLSTM** was the NLP default before Transformers. Downside: needs the whole sequence first, so it doesn't suit live speech.

## Deep RNNs

Stack recurrent layers: `a[l]<t> = g(W_a[l] [a[l]<t-1>; a[l-1]<t>] + b_a[l])`. **Three layers is already deep** for RNNs (expensive along the time axis); sometimes add non-recurrent dense layers on top per time step.

## Related

- Theano implementation: [[LISA Tutorial - RNN for Slot Filling]].
- AI-Notes perspective: see the section below.

## AI-Notes perspective

[[ai-notes|AI-Notes]] summary: an RNN is a feed-forward network with a **feedback loop**, giving a short-term memory (the hidden state).

- **Why not an ANN?** Fixed input size: padding wastes compute and truncation loses information; whole inputs arrive at once, so order is lost.
- **Why not a CNN?** Built for spatial hierarchies; weak at long-range sequence dependencies.
- **Types**: one-to-one (single-word classification), one-to-many (image captioning), many-to-one (sentiment), many-to-many synchronous (POS, NER), many-to-many asynchronous (translation, summarization).
- **Why shared weights across time?** Keeps parameter count and compute manageable, and lets patterns learned at one position apply at all positions (temporal pattern recognition).
- **Main drawback**: short memory (context fades after about 10 steps) because of vanishing gradients through saturating activations. ReLU variants help a little; [[Long Short-Term Memory|LSTM]] is the real fix.
