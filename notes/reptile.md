# [On First-Order Meta-Learning Algorithms](https://arxiv.org/abs/1803.02999.pdf)

### Alex Nichol, Joshua Achiam and John Schulman

#### 4 Apr 2018

---

### Concept

This paper is heavily related to [Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks](https://arxiv.org/abs/1703.03400). (Also Reptile vs. MAML :D) It begins with showing a simpler implementation of FOMAML, which can actually be derived pretty easily. 

More interestingly, the Reptile algorithm is far simpler and yet seems to perform nearly as good as the original MAML. 

---

### Notes

- In OpenAI's implementation (see below), the metatraining tasks use far more 'shots' than in the test task; while this makes sense in the context of the algorithm, I'm not sure what that says in terms of fair comparison between Reptile and MAML as presented in the paper

---

### Ideas

- Again, can we combine this with learned optimizers or other metalearning approaches? See [Optimization as a model for few-shot learning](https://openreview.net/pdf?id=rJY0-Kcll) and [Learning to learn by gradient descent by gradient descent](https://arxiv.org/abs/1606.04474)
- With respect to the above point on fair comparison, there should probably be a benchmarking review on the different metalearning algorithms, paying extra attention to the metatraining task parameters

---

### PS

OpenAI's implementation [here](https://github.com/openai/supervised-reptile).

My reproduced implementation [here](https://github.com/greentfrapp/maml-reptile) for the sine regression toy experiment.