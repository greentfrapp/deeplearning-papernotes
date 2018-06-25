# [Rapid Adaptation with Conditionally Shifted Neurons](https://arxiv.org/abs/1706.03762)

### Tsendsuren Munkhdalai, Xingdi Yuan, Soroush Mehri, Adam Trischler

#### 7 Mar 2018 `ICML2018`

---

### Concept

Another meta-learning paper, one that I have overlooked while looking at the many meta-learning papers from Finn, Levine and co..

Some quick notes here first.

The paper introduces a new meta-learning algorithm, one that uses memory to store *conditionally shifted neurons* that is then retrieved using soft attention during test time to augment the task-specific network.

The memory matrix here contains the neuron-specific gradient information that can be subsequently selected during the test phase, depending on the test sample eg. if the test sample is similar to training sample A, we incorporate the gradient memory from A to adjust the network, before predicting the test sample.

---

### Notes

- It seems like during task-specific training, only the memory matrix is updated with each training sample corresponding to a key-value pair. There seems to be no backpropagation done to the task-specific network during the training/description phase, which makes this similar to the schemes used by Koch et. al ([2015](https://www.cs.cmu.edu/~rsalakhu/papers/oneshot1.pdf)) and Vinyals et. al ([2016](https://arxiv.org/pdf/1606.04080))
- But in contrast to Koch and Vinyals, the memory matrix here sort of serves as a replacement to task-specific gradient descent, which relates this to Ravi & Larochelle ([2017](https://openreview.net/pdf?id=rJY0-Kcll)) and Marcin et. al ([2016](https://openreview.net/pdf?id=rJY0-Kcll))
- **Of particular interest, this paper builds on Munkhdalai & Yu ([2017](https://arxiv.org/abs/1703.00837)) and that paper documents an experiment where the model transits from Omniglot to MNIST, where performance on Omniglot initially improves with new training solely on MNIST.** Not sure if that is also the case for this new simpler architecture but seems to be worth investigating, with relation to task-independent models.
- Adapts ideas from attention and memory-based architectures

---

### Ideas

- Consider the possibility of incorporating ideas from the Transformer eg. self-attending in the memory matrix
- As with the abovementioned algorithms, scaling and transiting from few-shot to big data might be unelegant
