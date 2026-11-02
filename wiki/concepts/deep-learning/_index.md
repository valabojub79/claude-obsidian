---
type: meta
title: "Deep Learning Concepts Index"
created: 2026-11-02
updated: 2026-11-02
tags:
  - meta
  - index
  - deep-learning
status: evergreen
related:
  - "[[index]]"
  - "[[Deep Learning]]"
---

# Deep Learning Concepts Index

Navigation: [[index]] | [[Deep Learning]] | [[concepts/_index|Concepts]] | [[sources/_index|Sources]]

Pages in `wiki/concepts/deep-learning/`: from [[deeplearning-ai-summary|DeepLearning.ai Summary]] and [[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]], with overlapping [[ai-notes|AI-Notes]] notes merged in as perspective sections.

## Hub (1)

- [[Deep Learning]]: Entry point to the deep learning and machine learning knowledge base built from four repositories (ingested 2026-11-02). (developing)

## DLAI course hubs (5)

- [[DLAI Course 1 - Neural Networks and Deep Learning]]: First course of Andrew Ng's Deep Learning Specialization, as summarized in DeepLearning.ai Summary. (developing)
- [[DLAI Course 2 - Improving Deep Neural Networks]]: Full title: (developing)
- [[DLAI Course 3 - Structuring Machine Learning Projects]]: The shortest course (two weeks), and the one with no math: (developing)
- [[DLAI Course 4 - Convolutional Neural Networks]]: Computer vision with deep learning, as summarized in DeepLearning.ai Summary. (developing)
- [[DLAI Course 5 - Sequence Models]]: The final course of the specialization (DeepLearning.ai Summary): (developing)

## LISA tutorials (14)

- [[LISA Tutorial - 1D Segmentation of Cortical Layers]]: Segment the 6 layers of the cerebral cortex in the BigBrain dataset (a 3D ultra-high-resolution brain reconstructed from 2D... (developing)
- [[LISA Tutorial - Convolutional Networks LeNet]]: A simplified LeNet-5 for MNIST in Theano. (developing)
- [[LISA Tutorial - Deep Belief Networks]]: Hinton, Osindero, Teh, 2006: (developing)
- [[LISA Tutorial - Denoising Autoencoders]]: Vincent et al., 2008. (developing)
- [[LISA Tutorial - Getting Started]]: The shared foundation for every tutorial in LISA Deep Learning Tutorials: (developing)
- [[LISA Tutorial - Hybrid Monte Carlo Sampling]]: Duane et al. 1987; Neal 1993. (developing)
- [[LISA Tutorial - LSTM Sentiment Analysis]]: Binary sentiment (positive or negative) on the IMDB Large Movie Review Dataset (Maas et al. 2011), in Theano. (developing)
- [[LISA Tutorial - Logistic Regression]]: The first algorithm tutorial in LISA Deep Learning Tutorials: (developing)
- [[LISA Tutorial - Multilayer Perceptron]]: One-hidden-layer Multilayer Perceptron on MNIST in Theano. (developing)
- [[LISA Tutorial - RNN for Slot Filling]]: Mesnil, He, Deng, Bengio (Interspeech 2013). (developing)
- [[LISA Tutorial - RNN-RBM Polyphonic Music]]: Boulanger-Lewandowski, Bengio, Vincent (ICML 2012). (developing)
- [[LISA Tutorial - Restricted Boltzmann Machines]]: p(x) = exp(-E(x)) / Z, with Z = sum_x exp(-E(x)) (the partition function). (developing)
- [[LISA Tutorial - Semantic Segmentation FCN and U-Net]]: Two tutorials (fcn_2D_segm, unet), implemented in Theano + Lasagne, with data loaded via fvisin/dataset_loaders. (developing)
- [[LISA Tutorial - Stacked Denoising Autoencoders]]: Bengio 2007 (stacked autoencoders) and Vincent 2008 (denoising version). (developing)

## Concepts (57)

- [[Activation Functions]]: The non-linearity g applied after each layer's linear step z = Wa + b. (developing)
- [[Attention Mechanism]]: Bahdanau, Cho, Bengio, 2014: (developing)
- [[Autoencoders]]: A network trained to reproduce its input through a code (hidden representation): (developing)
- [[BLEU Score]]: Bilingual Evaluation Understudy (Papineni et al. 2002). (developing)
- [[Backpropagation]]: Computing the gradient of the cost with respect to every parameter by applying the chain rule backward over a computation graph. (developing)
- [[Batch Normalization]]: Ioffe and Szegedy (2015). (developing)
- [[Beam Search]]: A heuristic search for the most likely output sequence. (developing)
- [[Bias and Variance]]: "Easy to learn, difficult to master." Diagnose from train and dev error, relative to a baseline (human-level or Bayes error): (developing)
- [[Classic CNN Architectures]]: Reading case studies is the fastest way to learn how to combine conv, pool and FC layers. (developing)
- [[Convolutional Neural Networks]]: Networks built from convolution, pooling and fully connected layers, designed for grid data such as images. (developing)
- [[Data Augmentation]]: Create extra training examples by applying label-preserving transformations. (developing)
- [[Data Mismatch]]: Deep learning is data-hungry, so training data often comes from a different distribution than the dev and test data you care... (developing)
- [[Deep L-Layer Neural Network]]: A fully connected network with L layers (the input layer is not counted). (developing)
- [[Deep Learning Frameworks]]: From-scratch NumPy is for understanding. (developing)
- [[Dropout]]: On each training iteration, randomly zero each hidden unit with probability 1 - keep_prob. (developing)
- [[End-to-End Deep Learning]]: Replace a multi-stage pipeline with one network mapping input directly to output. (developing)
- [[Energy-Based Models]]: Assign a scalar energy to every configuration; plausible configurations get low energy: (developing)
- [[Error Analysis]]: Manually inspect the examples your model gets wrong, so you know where effort will pay off before spending weeks on it. (developing)
- [[Evaluation Metrics and Dev Sets]]: Pick one number up front so you can rank ideas instantly. (developing)
- [[Face Recognition]]: You may have one photo per employee, and new people join constantly, so a softmax over K people doesn't work. (developing)
- [[Gated Recurrent Unit]]: Cho et al. 2014; Chung et al. 2014. (developing)
- [[Generative Adversarial Networks]]: Goodfellow et al., 2014. (developing)
- [[GloVe]]: Pennington, Socher, Manning, 2014. (developing)
- [[Gradient Checking]]: Verify a hand-written Backpropagation by comparing it against a numerical estimate. (developing)
- [[Gradient Descent]]: Iteratively move parameters a small step against the gradient of the cost: (developing)
- [[Human-Level Performance]]: avoidable bias = train error - human error (developing)
- [[Hyperparameter Tuning]]: 1. (developing)
- [[Inception Network and 1x1 Convolutions]]: On a 6x6x32 volume, a 1x1x32 filter is a tiny fully connected layer applied at every pixel across channels, followed by ReLU. (developing)
- [[Input Normalization]]: Rescale input features to zero mean and unit variance before training: (developing)
- [[Language Models and Sequence Generation]]: A language model assigns a probability to any sequence of words. (developing)
- [[Logistic Regression]]: A binary classifier, and the smallest possible neural network: (developing)
- [[Long Short-Term Memory]]: Hochreiter & Schmidhuber, 1997. (developing)
- [[Mini-Batch Gradient Descent]]: Split the training set into mini-batches X{t}, Y{t} and take a Gradient Descent step after each one. (developing)
- [[Multi-Task Learning]]: One network learns several tasks at once, sharing lower layers. (developing)
- [[Multilayer Perceptron]]: A feed-forward network of fully connected layers: (developing)
- [[Neural Style Transfer]]: Gatys et al., 2015. (developing)
- [[Object Detection]]: y = [p_c, b_x, b_y, b_h, b_w, c_1, ..., c_k] (developing)
- [[Optimization Algorithms]]: Improvements on plain Gradient Descent covered in DLAI Course 2, week 2. (developing)
- [[Orthogonalization]]: Design your tuning "knobs" so that each one affects exactly one thing, like the separate steering and speed controls of a car. (developing)
- [[Parameters vs Hyperparameters]]: Deep learning is empirical: (developing)
- [[Recurrent Neural Networks]]: 1. (developing)
- [[Regularization]]: Techniques that reduce variance (overfitting), usually at a small cost in training fit. (developing)
- [[Residual Networks]]: He et al., 2015. (developing)
- [[Semantic Segmentation]]: Predict a class for every pixel. (developing)
- [[Sequence to Sequence Models]]: Sutskever et al. 2014; Cho et al. 2014. (developing)
- [[Siamese Networks and Triplet Loss]]: Two (or three) copies of the same network with shared weights encode inputs into embeddings; a distance between embeddings... (developing)
- [[Softmax Regression]]: Generalizes Logistic Regression to C classes. (developing)
- [[Speech Recognition and CTC]]: A microphone records air-pressure changes over time. (developing)
- [[Text Preprocessing]]: Cleaning raw text before building embeddings or features. (developing)
- [[Train Dev Test Split]]: Dev and test only need to be big enough to tell models apart and give confidence in the final number. (developing)
- [[Transfer Learning]]: Reuse what a network learned on task A (lots of data) for task B (less data). (developing)
- [[Unsupervised Pretraining]]: Initialize a deep network by training it layer by layer without labels, then fine-tune the whole network on the supervised task. (developing)
- [[Vanishing and Exploding Gradients]]: In a deep network, activations and gradients are products of many per-layer factors, so they can shrink or grow exponentially... (developing)
- [[Vectorization and Broadcasting]]: Replace explicit Python for loops with whole-array operations (np.dot, np.exp, np.sum). (developing)
- [[Weight Initialization]]: If all weights start equal (say zero), every hidden unit computes the same function and receives the same update, forever. (developing)
- [[Word Embeddings]]: A one-hot vector o_j treats every word as unrelated: (developing)
- [[Word2Vec and Negative Sampling]]: Mikolov et al., 2013. (developing)

