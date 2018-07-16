# [Dynamic Few-Shot Visual Learning without Forgetting](https://arxiv.org/pdf/1804.09458)

### Spyros Gidaris & Nikos Komodakis

#### 25 Apr 2018 `CVPR2018`

---

### Concept

A few-shot learning paper that may have been unnoticed since it was published at CVPR and appears to be image-focused.

Metalearning papers often cite the analogy of humans learning to identify new objects with few examples. This paper attempts to follow through with the analogy, by placing emphasis on a metalearning system that *does not forget* a set of base categories, just as how humans do not forget simpler objects and base their acquisition of new knowledge and classes on these simpler objects.

To quote the paper:

> However, most prior methods neglect to fulfill two very important requirements for a good few-shot learning system: (a) the learning of the novel categories needs to be fast, and (b) to not sacrifice any recognition accuracy on the initial categories that the ConvNet was trained on, i.e., to not "forget" [...]

In order to accomplish both goals, the paper proposes a scheme that builds on a base classifier which is already trained on a set of base categories.

1. **Classification-weight Generator** - For most classification networks, the final logits layer is calculated by multiplying the high-level features from the previous layer by an M x N matrix, where M is the number of features and N is the number of classes. In other words, each row of the matrix corresponds to the weights for a particular class. Following that train of thought, if we want to add a new class, we might only need to calculate a new set of weights for that particular class. Furthermore, this new set of weights can be calculated as a weighted sum of the base weights.
2. **Cosine-similarity-based Classifier** - If we intend to incorporate the above idea of generating classification weights for new classes, the authors note that we have to change the classification model from dot-product-based to cosine-similarity-based. This is attributed to the difference in training process of the base weights and the novel weights, which appears to "impede the training process" (see Section 3.1). Instead, the classifier here uses cosine-similarity, which is effectively the same as the usual classifier, except that the vectors are normalized before the dot-product. The authors also use a learned scalar parameter to scale the resulting dot-product (see Equation 4).

Following the cosine-similarity-based classifier, the "weights" for a new class can be interpreted as the average or a weighted average of the feature embeddings of the class' training samples.

---

### Notes

- It is not clear whether it is entirely fair to compare against other metalearning algorithms when the training process is rather different. In this case, the authors' algorithm is trained on all 64 classes as base categories, whereas typical metalearning algorithms are trained on all 64 classes across several N-way k-shot training episodes. On one hand, the training set is identical. On the other hand, one can't help but feel that being able to see the entire training dataset offers an unfair advantage.
- Because we use cosine-similarity, each "weight vector" for a particular class corresponds to the "anchor vector" for the class (borrowing the term from Prototypical Networks by Snell et al. ([2017](https://arxiv.org/abs/1703.05175))). In other words, the weight vector can be seen as the average feature vector for that class, such that samples from that class align best with this representation, hence achieving optimal classification results.

---

### Ideas



---

### PS

The authors have an implementation [here](https://github.com/gidariss/FewShotWithoutForgetting)

This idea also follows concurrent work by Qi et al. ([2017](https://arxiv.org/pdf/1712.07136)).