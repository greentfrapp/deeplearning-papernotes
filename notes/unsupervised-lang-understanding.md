# [Improving Language Understanding by Generative Pre-Training](https://blog.openai.com/language-unsupervised/)

### Alec Radford, Karthik Narasimhan, Tim Salimans, Ilya Sutskever

#### 11 June 2018

---

### Concept

I mentioned this in the [notes](https://github.com/greentfrapp/deeplearning-papernotes/blob/master/notes/transformer.md) on Attention is All You Need.

Following the Transformer model introduced by Vaswani et. al ([2017](https://arxiv.org/abs/1706.03762)) and adapting the decoder-only idea from Liu et. al ([2018](https://arxiv.org/abs/1801.10198)), this paper uses only the Decoder layer (minus the Encoder-Decoder Attention sublayer) for language modeling.

Essentially, by training the model to predict subsequent tokens from a huge dataset, the **language model** obtained is an analogy to the mechanism in your brain that kicks in when you hear 

> I run 5km yesterday.

and notice something wrong instantly (ie. *ran* instead of *run* or *everyday* instead of *yesterday*).

Two main things of interest.

1. The paper demonstrates what sheer compute and large data resources can do, with a pretty deep (37-layer/12xDecoder) model and 1 month pretraining on 8 GPUs and the resulting SOTA results by fine-tuning the singular trained model on all sorts of language tasks. Thankfully they are releasing the model and the source code [here](https://github.com/openai/finetune-transformer-lm)!

2. The idea of training a language model and then adapting it for a different task is actually not new. Just recently, Trinh & Le ([2018](https://arxiv.org/pdf/1806.02847)) also demonstrated the same idea on the Pronoun Disambiguation and Winograd Schema challenges. The overall method is similar, training language models on large and diverse corpora (TIL the plural of corpus) and adapting it to the task.

Here's a simple and clear example for the task adaptation, taken from Trinh & Le ([2018](https://arxiv.org/pdf/1806.02847)), who extracted this from the Winograd Schema challenge:

> The trophy doesn’t fit in the suitcase because it is too big. What is too big?
>
> Answer 0 : the trophy. Answer 1 : the suitcase

The simple but perhaps unintuitive method is to simply substitute *it* in the sentence with both options ie.

> The trophy doesn’t fit in the suitcase because **the trophy** is too big.
>
> The trophy doesn’t fit in the suitcase because **the suitcase** is too big.

Then we can simply use a trained language model to evaluate the likelihood of both sentences and then select the more probably option. 

---

### Notes

- Although the dataset used here is rather big and the sequences are up to 512 tokens long, the paper does not seem to adopt any special mitigations such as those introduced by Liu et. al ([2018](https://arxiv.org/abs/1801.10198)), such as local attention (dividing the sequences into subsequences for calculating attention) and memory-compressed attention (reducing keys and values using convolution). It is likely that such methods entail a tradeoff between performance and memory.
- The paper also mentions using learned positional encodings rather than the sinusoidal version proposed by Vaswani et. al ([2017](https://arxiv.org/abs/1706.03762)). I'm particularly curious regarding this. Yes, intuitively, learned encodings should perform equal to or better than fixed encodings. But Vaswani et. al also mentioned that the sinusoidal encodings could help with longer-than-training sequences. Might be interesting to actually test that latter claim.

---

### Ideas

- This paper might be some indication that the potential of the Transformer model has yet to be fully exploited. See [notes](https://github.com/greentfrapp/deeplearning-papernotes/blob/master/notes/transformer.md) on Transformer.
