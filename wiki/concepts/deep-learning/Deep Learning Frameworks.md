---
type: concept
title: "Deep Learning Frameworks"
created: 2026-11-02
updated: 2026-11-02
tags:
  - concept
  - deep-learning
  - tooling
complexity: beginner
domain: deep-learning
status: developing
address: c-000147
related:
  - "[[DLAI Course 2 - Improving Deep Neural Networks]]"
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
sources:
  - "[[.raw/repos/DeepLearning.ai-Summary/2- Improving Deep Neural Networks/Readme.md]]"
---

# Deep Learning Frameworks

## Why use one

From-scratch NumPy is for understanding. Frameworks give automatic differentiation (you write only the forward pass), one-line optimizer swaps, GPU kernels and graph-level optimizations.

## Choosing (Ng's criteria)

1. Ease of programming (development **and** deployment).
2. Running speed.
3. Truly open: open source **with good governance**, not just today's license.

The 2017 list in DLAI: Caffe/Caffe2, CNTK, DL4J, Keras, Lasagne, MXNet, PaddlePaddle, TensorFlow, Theano, Torch/PyTorch. Since then PyTorch and JAX dominate research, and TensorFlow/Keras persists in production. Theano (used by [[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]) was discontinued in 2017.

## TensorFlow 1.x pattern (as taught in 2017)

```python
w = tf.Variable(0, dtype=tf.float32)
x = tf.placeholder(tf.float32, [3, 1])
cost = x[0][0]*w**2 + x[1][0]*w + x[2][0]
train = tf.train.GradientDescentOptimizer(0.01).minimize(cost)
with tf.Session() as s:
    s.run(tf.global_variables_initializer())
    for _ in range(1000):
        s.run(train, feed_dict={x: coeffs})
```

Steps: create tensors, write ops, initialize, create a session, run. Pass logits (`Z[L]`, not `A[L]`) to fused losses such as `sigmoid_cross_entropy_with_logits` for numerical stability.

> [!stale] TF1 API
> `placeholder`, `Session` and `tf.contrib` were removed in TensorFlow 2.x (eager by default). The concepts carry over; the code doesn't.
