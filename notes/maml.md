# [Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks](https://arxiv.org/abs/1703.03400)

### Chelsea Finn, Pieter Abbeel, Sergey Levine

#### 18 Jul 2017 `ICML2017`

---

### Concept

This paper introduces a new approach to metalearning, closely related to the idea of transfer learning (common in image classification). Essentially, the MAML algorithm seeks to learn a good initialization for a model's weights, allowing the model to quickly achieve good results after few gradient steps on small datasets. 

The algorithm itself is relatively elegant and intuitive, the main challenge being the second derivative when doing the meta-optimizing, which is also discussed in the paper. Of note, the paper shows empirically that first-order MAML (FOMAML) performs rather well despite discarding the abovementioned second derivatives.

The algorithm seems to be founded on the belief that for similar tasks, optimal network parameters lie fairly close to each other in the parameter space, such that there exists an optimal initialization that can be learned. 

Also interesting, the paper proposes that the surprisingly good performance of FOMAML might be attributed to the highly linear nature of the models, a similar theme with Adversarial Examples.

---

### Notes

- In Finn's implementation, the model is unrolled to allow the calculation of the second derivatives; when I tried implementing this, I notice that if we unroll it too many steps and if the learning rate is too high, the gradient tends to explode, echoing the previous problem with optimizing for RNNs
- OpenAI also has a recent work expanding on this idea (see [Reptile](https://blog.openai.com/reptile/))

---

### Ideas

- Can we combine this with learned optimizers or other metalearning approaches? See [Optimization as a model for few-shot learning](https://openreview.net/pdf?id=rJY0-Kcll) and [Learning to learn by gradient descent by gradient descent](https://arxiv.org/abs/1606.04474)

---

### PS

Finn's implementation [here](https://github.com/cbfinn/maml).

My reproduced implementation [here](https://github.com/greentfrapp/maml-reptile) for the sine regression toy experiment.