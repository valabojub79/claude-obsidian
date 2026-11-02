---
type: source
title: "Deep Learning Paper Notes"
source_type: repository
author: "Denny Britz"
date_published: 2018-02-01
date_ingested: 2026-11-02
created: 2026-11-02
updated: 2026-11-02
url: "https://github.com/dennybritz/deeplearning-papernotes"
commit: 7195945731e849d88f4702ac432973c57fc93e97
license: "none stated"
confidence: high
tags:
  - source
  - deep-learning
  - paper-notes
status: ingested
address: c-000126
related:
  - "[[Denny Britz]]"
  - "[[Deep Learning]]"
  - "[[Attention Mechanism]]"
  - "[[Sequence to Sequence Models]]"
sources:
  - ".raw/repos/deeplearning-papernotes/"
key_claims:
  - "2014-2017 deep NLP converged on attention-based encoder-decoders, subword units and pretraining"
  - "Many papers win by small margins with added complexity; simple baselines (deep LSTMs, n-grams) are often competitive"
  - "Perplexity and BLEU are imperfect proxies; dialogue and generation need better evaluation"
---

# Deep Learning Paper Notes (Denny Britz)

Denny Britz's 2015-2018 summaries of deep learning papers (he is also the author of the WildML blog). Two parts:

1. **99 detailed notes** (`notes/*.md`): a TL;DR, key points and a candid critique. Each one is a wiki page in `wiki/sources/dl-papers/` (index below).
2. **A reading list of 627 papers** by month (2011 to Feb 2018), mostly links only. Summarized in [[deep-learning-reading-list|Deep Learning Reading List 2013-2018]].

Snapshot at `7195945`, stored locally (gitignored) at `.raw/repos/deeplearning-papernotes/`. **No license is stated**, so the wiki pages paraphrase rather than copy, and attribute the critique to Denny Britz.

## Big themes across the notes

- **NLP centered, 2015-2017**: 22 machine-translation papers trace the path from fixed-vector seq2seq ([[Sequence to Sequence Learning with Neural Networks]]) through attention ([[Neural Machine Translation by Jointly Learning to Align and Translate]], [[Effective Approaches to Attention-Based Neural Machine Translation]]) and subword units ([[Neural Machine Translation of Rare Words with Subword Units]]) to multilingual zero-shot systems ([[Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation]]).
- **Pretraining before BERT**: [[Semi-Supervised Sequence Learning]], [[Skip-Thought Vectors]], [[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data]], [[Distributed Representations of Sentences and Documents]].
- **Ingredients of the Transformer, seen separately**: attention, multi-row self-attention ([[A Structured Self-Attentive Sentence Embedding]]), memory hops ([[End-To-End Memory Networks]]), [[Layer Normalization]], residuals ([[Deep Residual Learning for Image Recognition]]), and the warmup with inverse-square-root learning-rate schedule ([[Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer]]).
- **Exposure bias and sequence-level training**: [[An Actor-Critic Algorithm for Sequence Prediction]], [[Professor Forcing - A New Algorithm for Training Recurrent Networks]], [[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]], [[Sequence-Level Knowledge Distillation]].
- **Deep RL exploration and sample efficiency**: [[Hindsight Experience Replay]], [[Noisy Networks for Exploration]], [[Reinforcement Learning with Unsupervised Auxiliary Tasks]], [[Deep Q-learning from Demonstrations]].

## Denny's recurring critiques (worth applying to any paper)

1. Are comparisons fair? Matched parameter counts, the same pretrained embeddings and external data for the baselines, equal tuning effort.
2. Report variance, training time and wall-clock speed, not only theoretical complexity.
3. Hyperparameters added by the method: how sensitive are results to them, and how were they chosen?
4. Does the complexity beat a well-tuned simple baseline (a deep LSTM, n-grams, more hidden units)?
5. Are the metrics meaningful (BLEU for dialogue, perplexity when avoiding high-probability outputs, bits per character)?
6. Missing ablations and obvious experiments (bidirectional variants, other datasets, longer sequences).

## Index of the 99 notes by topic

### Neural Machine Translation (22)

- [[A Character-Level Decoder without Explicit Segmentation for Neural Machine Translation]] (2016): Chung, Cho and Bengio keep a BPE subword encoder but decode at the character level, with no explicit segmentation.
- [[Achieving Open Vocabulary Neural Machine Translation with Hybrid Word-Character Models]] (2016): Luong and Manning build a fast word-level NMT where `<unk>` tokens are handled by character-level RNNs.
- [[Dual Learning for Machine Translation]] (2016): He et al. use monolingual data through a two-agent "dual game" trained with policy gradient:
- [[Effective Approaches to Attention-Based Neural Machine Translation]] (2015): Luong, Pham and Manning compare global attention (over all source words) and local attention (a window around a predicted position).
- [[Fully Character-Level Neural Machine Translation without Explicit Segmentation]] (2016): Lee, Cho and Hofmann build char-to-char NMT.
- [[Google's Multilingual Neural Machine Translation System - Enabling Zero-Shot Translation]] (2016): Johnson et al. take the unchanged GNMT architecture and prepend a target-language token (for example `<2fr>`) to the input.
- [[Incorporating Copying Mechanism in Sequence-to-Sequence Learning]] (2016): CopyNet (Gu et al.) lets a seq2seq decoder either *generate* from the vocabulary or *copy* a token from the source.
- [[Learning Phrase Representations using RNN Encoder-Decoder for Statistical Machine Translation]] (2014): Cho et al. introduce the RNN encoder-decoder (encode to a fixed vector, decode a variable-length output) and the GRU cell.
- [[Learning to Translate in Real-time with Neural Machine Translation]] (2016): Gu et al. do simultaneous translation.
- [[Multi-Way, Multilingual Neural Machine Translation with a Shared Attention Mechanism]] (2016): Firat, Cho and Bengio build one NMT model for N x M language pairs, with per-language encoders and decoders and a single shared attention mechanism.
- [[Multi-task Sequence to Sequence Learning]] (2015): Luong et al. show that jointly training seq2seq tasks improves a reference task.
- [[Neural Machine Translation by Jointly Learning to Align and Translate]] (2014): Bahdanau, Cho and Bengio introduce attention.
- [[Neural Machine Translation in Linear Time]] (2016): Kalchbrenner et al.'s ByteNet: a WaveNet-style architecture for translation.
- [[Neural Machine Translation of Rare Words with Subword Units]] (2015): Sennrich, Haddow and Birch adapt Byte Pair Encoding (BPE) to split rare words into subword units, giving open-vocabulary NMT without UNK...
- [[Neural Machine Translation with Reconstruction]] (2016): Tu et al. add a reconstructor RNN that regenerates the source from the decoder's hidden states (attending over them).
- [[Neural Machine Translation with Recurrent Attention Modeling]] (2016): Standard attention ignores where it attended before, though that history predicts the next focus.
- [[On Using Very Large Target Vocabulary for Neural Machine Translation]] (2014): Jean et al. use importance sampling to train NMT with a very large target vocabulary.
- [[On the Properties of Neural Machine Translation - Encoder-Decoder Approaches]] (2014): Cho et al. analyze early encoder-decoder NMT.
- [[Outrageously Large Neural Networks - The Sparsely-Gated Mixture-of-Experts Layer]] (2017): Shazeer et al. add a Sparsely-Gated Mixture-of-Experts layer: up to thousands of feed-forward experts and a trainable gate that routes each...
- [[Recurrent Neural Machine Translation]] (2016): Replace Bahdanau attention with a recurrent (GRU) attention to capture attention history and mitigate the coverage problem.
- [[Sequence to Sequence Learning with Neural Networks]] (2014): Sutskever, Vinyals and Le's seq2seq paper: a deep 4-layer LSTM encoder-decoder (1000 cells per layer, 1000-d embeddings, 160k source and 80k...
- [[Sequence-Level Knowledge Distillation]] (2016): Kim and Rush extend distillation to NMT:

### Reinforcement Learning (13)

- [[An Actor-Critic Algorithm for Sequence Prediction]] (2016): Train seq2seq models with actor-critic RL.
- [[Deep Q-learning from Demonstrations]] (2017): DQfD pretrains a DQN agent on human demonstrations with four losses, then keeps learning online with demonstrations and agent transitions in one...
- [[Deep Reinforcement Learning with a Natural Language Action Space]] (2015): He et al.'s DRRN (Deep Reinforcement Relevance Network) for text games.
- [[Exploration - A Study of Count-Based Exploration for Deep Reinforcement Learning]] (2016): "#Exploration": add an exploration bonus `beta / sqrt(n(phi(s)))` for rarely visited states.
- [[Hindsight Experience Replay]] (2017): Andrychowicz et al. (OpenAI) tackle sparse binary rewards.
- [[Learning Online Alignments with Continuous Rewards Policy Gradient]] (2016): Luo et al. train an RNN with a hard, online attention decision (emit an output at this step or not) using policy gradients, so it doesn't need the...
- [[Noisy Networks for Exploration]] (2017): Fortunato et al. (DeepMind) add learned parametric noise to network weights (`w = mu + sigma * eps`, with `mu` and `sigma` trained by gradient...
- [[Progressive Neural Networks]] (2016): Rusu et al. (DeepMind) do transfer without forgetting.
- [[Recurrent Models of Visual Attention]] (2014): Mnih et al.'s Recurrent Attention Model (RAM): an RNN takes a low-resolution, multi-scale glimpse, then chooses where to look next and,...
- [[Reinforcement Learning with Unsupervised Auxiliary Tasks]] (2016): Jaderberg et al. (DeepMind) propose UNREAL: A3C plus auxiliary tasks sharing the CNN and LSTM trunk.
- [[SeqGAN - Sequence Generative Adversarial Nets with Policy Gradient]] (2016): Yu et al. train a GAN for discrete sequences.
- [[Third-Person Imitation Learning]] (2017): Stadie, Abbeel and Sutskever learn a policy by watching a demonstrator from a different viewpoint (third person), unlike standard imitation, which...
- [[WebNav - A New Large-Scale Task for Natural Language Based Sequential Decision Making]] (2016): Nogueira and Cho propose a navigation task: starting from a Wikipedia page, follow links to find the page that contains a query (a few sentences),...

### Language Modeling (8)

- [[Character-Aware Neural Language Models]] (2015): Kim et al. feed an LSTM language model character-CNN word representations (via highway layers) instead of word embeddings.
- [[Contextual LSTM (CLSTM) Models for Large Scale NLP Tasks]] (2016): Append a topic/context vector to each LSTM input.
- [[Exploring the Limits of Language Modeling]] (2016): Jozefowicz et al. (Google Brain) scale LSTM language models on the One Billion Word benchmark: single-model perplexity 51.3 to 30.0, ensemble 41...
- [[Hierarchical Multiscale Recurrent Neural Networks]] (2016): Chung, Ahn and Bengio's HM-RNN learns hierarchical and temporal structure (characters, words, phrases) without being told the boundaries.
- [[Larger-Context Language Modeling]] (2015): Wang and Cho condition an LSTM language model on previous sentences.
- [[Pointer Sentinel Mixture Models]] (2016): Merity et al.'s Pointer Sentinel-LSTM mixes a softmax over the vocabulary with a pointer over the last `L` words of context:
- [[Recurrent Memory Network for Language Modeling]] (2016): Tran, Bisazza and Monz add a Memory Block (attention over the last `n` input words, keyed by the current hidden state) on top of an LSTM.
- [[Strategies for Training Large Vocabulary Neural Language Models]] (2015): Chen, Grangier and Auli compare softmax, hierarchical softmax, differentiated softmax (new), target sampling, NCE and self-normalization, under a...

### Vision and CNN Architectures (8)

- [[A Sensitivity Analysis of (and Practitioners' Guide to) Convolutional Neural Networks for Sentence Classification]] (2015): Zhang and Wallace run a large sweep (with variance estimates) over the hyperparameters of Kim's (2014) one-layer CNN across 7...
- [[Bridging the Gaps Between Residual Learning, Recurrent Neural Networks and Visual Cortex]] (2016): The visual cortex isn't hundreds of layers deep, but it is recurrent.
- [[Deep Networks with Stochastic Depth]] (2016): Huang et al. randomly drop entire residual blocks during training, keeping only the identity shortcut.
- [[Deep Residual Learning for Image Recognition]] (2015): He et al. introduce ResNets: shortcut connections let layers learn a residual `F(x) = H(x) - x`.
- [[ReNet - A Recurrent Neural Network Based Alternative to Convolutional Networks]] (2015): Visin et al. (LISA) replace conv and pool layers with four RNNs per layer sweeping over image patches vertically (both directions) and then...
- [[Show, Attend and Tell - Neural Image Caption Generation with Visual Attention]] (2015): Xu et al. add attention over CNN feature maps (lower conv layer, before pooling, so locations survive) to an LSTM caption decoder.
- [[Spatial Transformer Networks]] (2015): Jaderberg et al. (DeepMind) build a differentiable Spatial Transformer module that can be inserted anywhere in a network.
- [[Training Very Deep Networks]] (2015): Srivastava, Greff and Schmidhuber's Highway Networks: LSTM-style gates on feed-forward layers:

### Dialogue and Conversation (7)

- [[A Diversity-Promoting Objective Function for Neural Conversation Models]] (2015): Li et al. train with maximum likelihood but decode with Maximum Mutual Information (MMI) to avoid generic replies like "I don't know".
- [[A Neural Conversational Model]] (2015): Vinyals and Le train a plain seq2seq chatbot:
- [[A Neural Network Approach to Context-Sensitive Generation of Conversational Responses]] (2015): Sordoni et al. generate response `r` from (context `c`, message `m`) on 29M Twitter triples:
- [[Attention with Intention for a Neural Network Conversation Model]] (2015): Three RNNs for dialogue.
- [[Building End-To-End Dialogue Systems Using Generative Hierarchical Neural Network Models]] (2015): Serban et al. apply HRED (Hierarchical Recurrent Encoder-Decoder) to dialogue.
- [[End-to-End LSTM-Based Dialog Control Optimized with Supervised and Reinforcement Learning]] (2016): Williams and Zweig (Hybrid Code Networks precursor).
- [[Neural Responding Machine for Short-Text Conversation]] (2015): Shang, Lu and Li generate replies to Weibo posts (short-text conversation: single post to response, with no dialogue state).

### Memory and Attention Architectures (7)

- [[A Neural Attention Model for Abstractive Sentence Summarization]] (2015): Rush, Chopra and Weston's attention-based seq2seq model for headline generation (sentence-level abstractive summarization).
- [[Associative Long Short-Term Memory]] (2016): Augment LSTMs with an external key-value memory based on Holographic Reduced Representations (Plate 2003).
- [[End-To-End Memory Networks]] (2015): Sukhbaatar et al. (MemN2N).
- [[Latent Predictor Networks for Code Generation]] (2016): Ling et al. generate code from multiple predictors: attention-based character generation plus pointer networks that copy tokens from the input,...
- [[Neural Turing Machines]] (2014): Graves, Wayne and Danihelka couple a controller network (LSTM or MLP) with an external memory matrix accessed by differentiable read and write heads.
- [[Pointer Networks]] (2015): Vinyals, Fortunato and Jaitly's Ptr-Net: a seq2seq model whose outputs are positions in the input.
- [[Using Fast Weights to Attend to the Recent Past]] (2016): Ba, Hinton et al. add fast weights, a quickly decaying associative memory between slow weights (long-term) and hidden state (short-term):

### Other: Text Classification, Parsing, Decoding, Recommenders (7)

- [[Adversarial Training Methods for Semi-Supervised Text Classification]] (2016): Words are discrete, so apply adversarial perturbations to the word embeddings instead.
- [[Building Machines That Learn and Think Like People]] (2016): Lake, Ullman, Tenenbaum and Gershman compare deep learning to human learning through two challenges: recognizing new handwritten characters and...
- [[Diverse Beam Search - Decoding Diverse Solutions from Neural Sequence Models]] (2016): Split a beam of width `B` into `G` groups of `B/G`.
- [[Grammar as a Foreign Language]] (2014): Vinyals et al. treat constituency parsing as translation: a 3-layer seq2seq LSTM (256 units) with attention outputs the linearized parse tree.
- [[Semi-Supervised Sequence Learning]] (2015): Dai and Le pretrain an LSTM on unlabeled text, either as a sequence autoencoder (SA-LSTM: reconstruct the input from the final state) or as a...
- [[Sentence Level Recurrent Topic Model - Letting Topics Speak for Themselves]] (2016): An RNN topic model that respects word order and assumes all words in a sentence share a topic.
- [[Wide & Deep Learning for Recommender Systems]] (2016): Cheng et al. (Google) jointly train a wide linear model (memorization) and a deep network (generalization) for Google Play recommendations.

### Recurrent Architectures (6)

- [[A Recurrent Neural Network Without Chaos]] (2016): Laurent and von Brecht propose the Chaos-Free Network (CFN), a gated RNN much simpler than LSTM or GRU whose dynamics are provably non-chaotic and...
- [[A Unified Tagging Solution - Bidirectional LSTM Recurrent Neural Network with Word Embedding]] (2015): Wang et al. use one BiLSTM with task-independent inputs (word plus capitalization) for POS tagging, chunking and NER, with a decoder restricted to...
- [[Adaptive Computation Time for Recurrent Neural Networks]] (2016): Graves' Adaptive Computation Time (ACT) lets an RNN decide how many internal steps ("pondering") to spend on each input.
- [[Deep Knowledge Tracing]] (2015): Piech et al. model a student's evolving knowledge with an RNN or LSTM.
- [[Learning to Execute]] (2014): Zaremba and Sutskever show seq2seq LSTMs (2 layers of 400 cells, about 2.5M parameters) can evaluate short Python programs (loops, conditionals,...
- [[Target-Dependent Sentiment Classification with Long Short Term Memory]] (2015): Tang et al. classify sentiment toward a specific target in a sentence:

### Sentence and Document Embeddings (6)

- [[A Structured Self-Attentive Sentence Embedding]] (2017): Lin et al. (IBM and MILA) represent a sentence as a matrix: a BiLSTM's states `H`, combined by `r` different attention distributions:
- [[Distributed Representations of Sentences and Documents]] (2014): Le and Mikolov's Paragraph Vector (doc2vec) learns a fixed-length vector for text of any length by adding a per-paragraph embedding to a...
- [[Document Embedding with Paragraph Vectors]] (2015): Dai, Olah and Le evaluate Paragraph Vectors (PV-DBOW only, for efficiency) on large Wikipedia and arXiv retrieval tasks.
- [[Learning Document Embeddings by Predicting N-grams for Sentiment Classification of Long Movie Reviews]] (2015): DV-ngram: like Paragraph Vector, but the document vector alone must predict the document's words and n-grams (each n-gram treated as a token),...
- [[Skip-Thought Vectors]] (2015): Kiros et al. lift skip-gram to sentences.
- [[Supervised Learning of Universal Sentence Representations from Natural Language Inference Data]] (2017): Conneau et al.'s InferSent: train sentence encoders supervised on SNLI (entailment, contradiction, neutral) and transfer them.

### Character-Level Text Models (5)

- [[Alternative Structures for Character-Level RNNs]] (2015): Two ways to help character-level RNN language models: mixed (condition on a jointly trained word-level RNN, interpolating losses) and cond...
- [[Character-Level Convolutional Networks for Text Classification]] (2015): Zhang, Zhao and LeCun use a 9-layer CNN (6 conv/pool plus 3 fully connected layers) on one-hot characters, with fixed input length 1014.
- [[Efficient Character-Level Document Classification by Combining Convolution and Recurrent Layers]] (2016): ConvRec: a few conv layers over character embeddings, then an LSTM.
- [[Multilingual Language Processing From Bytes]] (2015): Gillick et al.'s Byte-to-Span (BTS): a seq2seq LSTM reads raw UTF-8 bytes from many languages (examples shuffled together) and outputs spans as...
- [[Text Understanding from Scratch]] (2015): Zhang and LeCun apply 6 and 9-layer (plus 3 fully connected) ConvNets to one-hot characters, with no word embeddings or word notion, on new large...

### Reading Comprehension and QA (4)

- [[Attention-over-Attention Neural Networks for Reading Comprehension]] (2016): For cloze-style QA (predict one missing word), the AoA reader:
- [[Natural Language Comprehension with the EpiReader]] (2016): Two-stage cloze-style QA trained end to end.
- [[SQuAD - 100,000+ Questions for Machine Comprehension of Text]] (2016): Rajpurkar et al. (Stanford) release the Stanford Question Answering Dataset: about 100k crowdsourced questions on about 500 Wikipedia articles,...
- [[Teaching Machines to Read and Comprehend]] (2015): Hermann et al. (DeepMind) build about 1M cloze-style QA examples from CNN and Daily Mail article bullet summaries: delete an entity and ask the...

### Training Techniques (3)

- [[Batch Normalization - Accelerating Deep Network Training]] (2015): Ioffe and Szegedy's *Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift*.
- [[Layer Normalization]] (2016): Ba, Kiros and Hinton normalize across the units of a layer for a single example, instead of across the batch.
- [[Recurrent Neural Network Regularization]] (2014): Zaremba, Sutskever and Vinyals show that Dropout works for LSTMs if applied only to non-recurrent connections (between layers at the same time...

### Generative Models (2)

- [[Generating Sentences from a Continuous Space]] (2015): Bowman et al.'s RNN variational autoencoder for sentences.
- [[Professor Forcing - A New Algorithm for Training Recurrent Networks]] (2016): Lamb, Goyal et al. address the train/test mismatch of teacher forcing with a GAN-style discriminator.

### Model Compression (1)

- [[Distilling the Knowledge in a Neural Network]] (2015): Hinton, Vinyals and Dean compress an ensemble (or big model) into a small one by training it on the teacher's soft targets: softmax with a raised...

## Related wiki pages

Concepts: [[Attention Mechanism]], [[Sequence to Sequence Models]], [[Beam Search]], [[Word Embeddings]], [[Residual Networks]], [[Batch Normalization]], [[Transfer Learning]]. Companion sources: [[deeplearning-ai-summary|DeepLearning.ai Summary]], [[lisa-deep-learning-tutorials|LISA Deep Learning Tutorials]], [[ai-notes|AI-Notes]].
