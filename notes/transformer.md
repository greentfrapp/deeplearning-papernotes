# [Attention is ALl You Need](https://arxiv.org/abs/1706.03762)

### Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz Kaiser, Illia Polosukhin

#### 6 Dec 2017 `NIPS2017`

---

### Concept

This landmark paper proposes the Transformer architecture, which is used in the paper to perform machine translation without the use of any recurrent or convolutional networks.

Building on the attention/alignment concept first introduced by Bahdanau et. al ([2014](https://arxiv.org/abs/1409.0473)), the Transformer architecture uses solely attention and dense layers. In Bahdanau et. al, a source sentence was encoded token-wise using a Bidirectional RNN. The decoder then has access to all the encoded tokens and an attention mechanism was used to focus on a subset of the input tokens for generating each output token. Phrased that way, one might question whether the Bidirectional RNN is even necessary, with two main considerations:

1. Since the decoder has access to all the embedded input tokens, do we need to use the Bidirectional RNN for embedding? Consider that the main advantage of the RNN is to embed a token in the context of the other tokens in the sentence. Since we have access to all input tokens during decoding, can we instead implicitly model this intra-sequence dependence?
2. Even if explicitly modeling the intra-sequence dependence does help, can we apply the same attention mechanism in the form of intra-attention or self-attention to embed the input sequence, rather than use a Bidirectional RNN?

While the RNN is immensely useful for modeling sequences, main disadvantages include the problems with backpropagation (vanishing/exploding gradients) and the difficulties with sustaining long-term dependencies especially in cases such as seq2seq models. Vaswani et. al's Transformer architecture, in doing away with RNNs, demonstrates SOTA performance on the WMT 2014 English-to-German and English-to-French translation tasks and does so in a fraction of previous training times.

As a brief summary, the Transformer model uses self-attention and dense layers for encoding input sequences, as well as an encoder-decoder attention for decoding from source to target languages.

Important details include multihead-attention, positional encodings and masking (detailed below).

---

### Notes

- It was introduced prior to this work, but the idea of dot-product attention is extremely intuitive when considering attention in terms of alignment between Query and Key ie. dot product of aligned (same direction) vectors is high and positive and vice versa. An important detail here is the scaling by root of the vector dimension, to prevent the dot product (and the subsequent softmax) from imploding.
- The paper introduces multihead-attention as a way of increasing the complexity of the original dot-product attention. A simple idea that nicely takes into account memory considerations.
- On first glance, at least to me, the idea of positional encodings may seem unimportant. More precisely, it is not immediately obvious that the Transformer (without positional encodings) does not consider positional dependence. This is a nontrivial aspect accomplished easily by RNNs and CNNs that could be taken for granted.
- The importance of masking was also unclear until I began implementing the Transformer for translation tasks. But once that was clarified, it also made clear how simple the training of the Transformer was!
- One huge plus point is the interpretability granted by the attention maps, which greatly improves the intuitive understanding of models and gives great visualizations to boot!

---

### Ideas

- Liu et. al ([2018](https://arxiv.org/abs/1801.10198)) and Radford et. al ([2018](https://blog.openai.com/language-unsupervised/)) adapted the Transformer architecture for use in language modeling, by discarding the Encoder layer and the ED-attention sublayer in the Decoder layer. This makes it apparent that while Vaswani et. al introduced a great general concept, the exact implementation was specifically catered for translation. It might be interesting to think about how we can change the architecture to replace other models previously dominated by RNNs.
- CNNs are in some way similar to attention, since we take a (soft and hard) weighted subset of inputs for generating outputs, in the form of kernels (where the size of the kernel is hard attention, the weights in the kernel is soft attention). Is there some form of advantage in pure attention over CNNs? How about combining CNNs with attention eg. SAGAN by Zhang et. al ([2018](https://arxiv.org/abs/1805.08318)).

---

### PS

My reproduced deconstructed implementation [here](https://github.com/greentfrapp/attention-primer) for several toy tasks.