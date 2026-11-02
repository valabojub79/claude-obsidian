---
type: concept
title: "Multilayer Perceptron"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - neural-networks
complexity: beginner
domain: deep-learning
status: developing
address: c-000183
related:
  - "[[Deep L-Layer Neural Network]]"
  - "[[LISA Tutorial - Multilayer Perceptron]]"
  - "[[Activation Functions]]"
sources:
  - "[[.raw/repos/DeepLearningTutorials/doc/mlp.txt]]"
  - "[[.raw/repos/AI-Notes/Deep Learning/Structured Data/Artificial Neural Net.md]]"
---

# Multilayer Perceptron (MLP)

A feed-forward network of fully connected layers: logistic regression applied on top of a **learned non-linear transformation** `Phi(x)` that makes the data linearly separable.

```
h(x) = s(b1 + W1 x)              # hidden layer, s = tanh or sigmoid (or ReLU today)
f(x) = G(b2 + W2 h(x))           # G = softmax for classification
```

- **Universal approximation**: one hidden layer of enough units can approximate any continuous function, but depth is often far more efficient (see [[Deep L-Layer Neural Network]]).
- Trained with [[Backpropagation]] and SGD.

Also called an "artificial neural network" or "fully connected network". DLAI's "shallow network" (one hidden layer) is an MLP.

## Pages

- Theano walkthrough with training tips: [[LISA Tutorial - Multilayer Perceptron]].
- Generalization to L layers: [[Deep L-Layer Neural Network]].
- AI-Notes perspective: see the section below.

## AI-Notes perspective (interview Q&A)

From [[ai-notes|AI-Notes]] (yuvraaj2002, based on CampusX videos):

- **Neuron** = weighted sum, then activation. A network of them is a neural network.
- **Why neural nets over classical ML?** Performance keeps rising with data (classical models plateau); they handle high-dimensional complex data; **hierarchical learning** (generic features early, specific later), which is what makes transfer learning possible.
- **Why the boom?** More data, plus cheap powerful GPUs.
- **Perceptron**: a single neuron with a step activation. Binary only, and it **can't solve XOR** (not linearly separable). The fix is multiple layers with smooth activations (sigmoid, tanh, ReLU), which handles regression and non-linear classification too.
- **Learnable parameters**: weights and biases. **Forward pass** predicts; **backward pass** updates parameters to reduce error.
- **Loss vs cost**: loss is per example; cost is the average over the dataset (same as DLAI).
- Vanishing gradients with sigmoid: its derivative is at most 0.25, so chained products shrink. The fix is other activations (see [[Vanishing and Exploding Gradients]]).
