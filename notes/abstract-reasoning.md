# [Measuring Abstract Reasoning in Deep Neural Networks](https://arxiv.org/abs/1807.04225)

### David G.T. Barrett, Felix Hill, Adam Santoro, Ari S. Morcos, Timothy Lillicrap

#### 11 Jul 2018 `ICML2018`

---

### Concept

IQ test for AI! The main contribution of the paper is the introduction of a dataset meant to assess logical generalization and relational reasoning, essentially the same as common IQ tests for humans. The dataset takes inspiration from Raven's Progressive Matrices, a common basic visual test meant to assess logical ability.

The paper also describes in detail the methodology for designing and automatically generating the dataset. It also shows the performance of several popular models (including ResNet and LSTM). Finally, the authors introduce a simple model, named Wild Relation Network (WReN) after John Raven's wife, that shows the best performance, although with much room for improvement in certain areas.

The WReN model is based on the authors' previous work on Relation Networks ([Santoro et al., 2017](https://arxiv.org/abs/1706.01427)). In this case, instead of treating image patches as objects, each (context and answer) panel in a test is treated as an object and encoded independently (ie. 8 context panels and 8 answers giving 16 encodings). Each answer panel encoding is fed in conjunction with all the context panels to a relation network, with the output being a score for that particular answer. This is done 8 times, once for each answer, and the final prediction is taken as a softmax over the 8 output scores.

Specifically, just as in the Relation Networks paper, the relation network here considers all possible pairs of inputs (9 object inputs - 8 context and 1 answer - giving 81 possible pairs).

---

### Notes

- An interesting thing to point out - the context-blind ResNet, which is exposed only to the answer panels, is able to achieve 22.4% accuracy, significantly above pure random chance of 12.5%. This seems to have been mentioned in other works such as the CLEVR dataset ([Johnson et al., 2016](https://arxiv.org/abs/1612.06890)) and VQA dataset ([Agrawal et al., 2015](https://arxiv.org/abs/1505.00468)) and I recall seeing some form of this behavior exhibited from personal experience. Should take this into account for future work.

---

### PS

The dataset is available [here](https://github.com/deepmind/abstract-reasoning-matrices).