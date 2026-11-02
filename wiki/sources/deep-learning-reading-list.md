---
type: source
title: "Deep Learning Reading List 2013-2018"
source_type: reading-list
author: "Denny Britz"
date_ingested: 2026-11-02
created: 2026-11-02
updated: 2026-11-02
url: "https://github.com/dennybritz/deeplearning-papernotes#readme"
tags:
  - source
  - deep-learning
  - reading-list
status: ingested
address: c-000127
related:
  - "[[deeplearning-papernotes|Deep Learning Paper Notes]]"
  - "[[Deep Learning]]"
sources:
  - "[[.raw/repos/deeplearning-papernotes/README.md]]"
---

# Deep Learning Reading List 2013-2018

The README of [[deeplearning-papernotes|Deep Learning Paper Notes]] lists **627 papers** by month, mostly as arXiv, code and blog links. The 99 with detailed notes have their own pages; this page maps the rest so you can find it without opening the raw list (`.raw/repos/deeplearning-papernotes/README.md`).

## Volume by year

| Year | Papers | Comment |
|------|--------|---------|
| 2011-2013 | 6 | Classics (word2vec era) |
| 2014 | 21 | seq2seq, attention, GANs begin |
| 2015 | 83 | ResNet, BatchNorm, NMT boom |
| 2016 | 250 | Peak NLP and deep RL; generative models |
| 2017 | 242 | Transformers, GAN zoo, PPO, AlphaGo Zero |
| 2018 (Jan-Feb) | 25 | ULMFiT, IMPALA, SAC; list stops |

## Landmarks in the list (no detailed note)

Paper pages don't exist for these; they're good next reads, ordered by theme.

### Architectures that stuck

- [Attention Is All You Need](https://arxiv.org/abs/1706.03762) (2017-06): the Transformer. See [[Transformer Architecture]].
- [Convolutional Sequence to Sequence Learning](https://arxiv.org/abs/1705.03122) (2017-05)
- [Xception](https://arxiv.org/abs/1610.02357) (2016-10), [Squeeze-and-Excitation Networks](https://arxiv.org/abs/1709.01507) (2017-09)
- [Self-Normalizing Neural Networks](https://arxiv.org/abs/1706.02515) (SELU, 2017-06)
- [Dynamic Routing Between Capsules](https://arxiv.org/abs/1710.09829) (2017-10)
- [One Model To Learn Them All](https://arxiv.org/abs/1706.05137) (2017-06)
- [Neural Architecture Search with RL](http://openreview.net/forum?id=r1Ue8Hcxg) (2016-11)

### Generative models

- [DCGAN](http://arxiv.org/abs/1511.06434) (2015-11), [Improved Techniques for Training GANs](http://arxiv.org/abs/1606.03498), [InfoGAN](http://arxiv.org/abs/1606.03657) (2016-06)
- [pix2pix: Image-to-Image Translation](https://arxiv.org/abs/1611.07004) (2016-11), [StarGAN](https://arxiv.org/abs/1711.09020), [Progressive Growing of GANs](http://research.nvidia.com/) (2017-10/11)
- [PixelRNN](http://arxiv.org/abs/1601.06759), [PixelCNN decoders](http://arxiv.org/abs/1606.05328), [WaveNet](https://arxiv.org/abs/1609.03499) (2016)
- [VQ-VAE: Neural Discrete Representation Learning](https://arxiv.org/abs/1711.00937) (2017-11), [Deep Image Prior](https://sites.skoltech.ru/app/data/uploads/sites/25/2017/11/deep_image_prior.pdf) (2017-11)

See [[Generative Adversarial Networks]].

### Speech

- [Deep Speech 2](http://arxiv.org/abs/1512.02595) (2015-12), [Deep Voice](https://arxiv.org/abs/1702.07825) and Deep Voice 3 (2017), [Tacotron 2](https://arxiv.org/abs/1712.05884) (2017-12). See [[Speech Recognition and CTC]].

### Reinforcement learning

- [PPO](https://openai-public.s3-us-west-2.amazonaws.com/blog/2017-07/ppo/ppo-arxiv.pdf) (2017-07), [Rainbow](https://arxiv.org/abs/1710.02298) (2017-10), [Distral](https://arxiv.org/abs/1707.04175), [IMPALA](https://arxiv.org/abs/1802.01561) (2018-02), [Soft Actor-Critic](https://arxiv.org/abs/1801.01290) (2018-01)
- AlphaGo Zero, *Mastering the game of Go without Human Knowledge* (Nature, 2017-10), and [AlphaZero for chess and shogi](https://arxiv.org/abs/1712.01815) (2017-12); [DeepStack](https://arxiv.org/abs/1701.01724) (poker, 2017-01)

### NLP

- [ULMFiT: Fine-tuned Language Models for Text Classification](https://arxiv.org/abs/1801.06146) (2018-01): pretrain an LM, then fine-tune (see [[Transfer Learning]]).
- [Generating Wikipedia by Summarizing Long Sequences](https://arxiv.org/abs/1801.10198) (2018-01): a decoder-only Transformer, an early sign of the GPT direction.

### Theory, meta-learning, perspective

- [Understanding deep learning requires rethinking generalization](https://arxiv.org/abs/1611.03530) (2016-10): networks memorize random labels.
- [Learning to learn by gradient descent by gradient descent](http://arxiv.org/abs/1606.04474) (2016-06)
- [The Matrix Calculus You Need For Deep Learning](https://arxiv.org/abs/1802.01528v2) (2018-02)
- [Deep Learning: A Critical Appraisal](https://arxiv.org/abs/1801.00631) (Marcus, 2018-01); compare [[Building Machines That Learn and Think Like People]].

> [!gap] Not ingested individually
> The other ~590 list entries are links without notes. Ingest any of them on demand ("ingest https://arxiv.org/abs/...") to get a full paper page.
