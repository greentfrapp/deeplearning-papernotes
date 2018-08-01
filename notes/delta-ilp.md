# [Learning Explanatory Rules from Noisy Data](https://arxiv.org/abs/1711.04574)

### Richard Evans, Edward Grefenstette

#### 25 Jan 2018 `JAIR`

---

### Concept

This paper integrates the advantage of inductive reasoning in symbolic programming with the robustness of artificial neural networks.

The context is that in symbolic programming, the values/choices of atoms/clauses are typically binary/discrete, which makes the optimization process rather non-differentiable.

The final algorithm echoes the theme of optimizing a soft distribution over modules, somewhat similar to Google's AutoML [project](https://arxiv.org/abs/1707.07012) by Zoph et al. (2018). In this case, the values of atoms are represented as continuous variables which can take on any value from 0 to 1. Rather than assigning Boolean flags to possible clauses, the model outputs a probability distribution over all clauses, which can be sampled from, in order to derive at the solution.

---

### Notes

- The interesting this here is the slightly more philosophical section where the authors show how conventional neural networks are unable to solve a toy task - given two MNIST images, identify the image that represents the larger value. Specifically, the trained model performs poorly on unseen MNIST pairs. This is elaborated in DeepMind's [blog post](https://deepmind.com/blog/learning-explanatory-rules-noisy-data/). While I was not surprised by this, it was interesting to try to understand why neural networks perform poorly on tasks requiring inductive logic and then realize how much prior knowledge we use as humans. In the case of the toy example, we can see that if we replace every digit with a random symbol, say a random Roman alphabet and give the same task (without the inequality sign) to humans, any human is likely to perform poorly as well. The advantage of inductive logic lies in the use of strong priors in the form of the ground atoms, that can be used for higher-level inference and extrapolation.
