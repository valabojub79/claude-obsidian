---
type: entity
title: "Theano"
entity_type: product
role: "Python library for symbolic tensor computation and automatic differentiation (2007-2017)"
first_mentioned: "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
created: 2026-11-02
updated: 2026-11-02
tags:
  - entity
  - product
  - deep-learning
  - tooling
status: developing
address: c-000408
related:
  - "[[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]]"
  - "[[Deep Learning Frameworks]]"
  - "[[Yoshua Bengio]]"
sources:
  - ".raw/repos/DeepLearningTutorials/"
---

# Theano

Developed at Montréal's LISA lab; one of the first deep-learning frameworks. Model: define a **symbolic graph**, then `theano.function` **compiles** it (with graph optimizations such as `log(sigmoid)` to softplus) to CPU or GPU code; `T.grad` provides **automatic differentiation**; `scan` handles loops and recurrence; **shared variables** hold state on the GPU.

All code in the [[lisa-deep-learning-tutorials|LISA tutorials]] uses it (segmentation tutorials via **Lasagne** on top). Its define-then-run design shaped TensorFlow 1.x ([[Deep Learning Frameworks]]).

Development stopped in 2017; successors are Aesara and **PyTensor** (used by PyMC). Practical gotchas recorded in the tutorials: store datasets as shared `floatX` for GPU speed; Theano function arguments are named by the *Theano variable* names; pickle arrays, not compiled functions ([[LISA Tutorial - Getting Started]]).
