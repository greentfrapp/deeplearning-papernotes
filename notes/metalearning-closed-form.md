# [Meta-learning with Differentiable Closed-form Solvers](https://arxiv.org/abs/1805.08136)

### Luca Bertinetto, João F. Henriques, Philip H.S. Torr, Andrea Vedaldi

#### 25 Apr 2018

---

### Concept

Similar to many other meta-learning papers, the authors here divide the meta-learner into a feature extractor and a classifier layer, where the feature extractor can be a multi-layer CNN and the classifier layer is a single layer or a simple linear transformation of the extracted features.

The novelty here is that the authors solve for the weights of the classifier layer using a differentiable process. This means that for each meta-training step, we can easily backpropagate through this process. Essentially, for each episode, we use the training set to solve for the weights of the classifier layer (either ridge regression or logistic regression). We then calculate the loss on the test set and backpropagate that through the entire network. Since the solver does not have any trainable parameters, we are only updating the weights of the feature extractor.

The final result from the meta-training is a feature extractor that generates features that are amenable to the weights-solver, such that the calculated weights work well on an unseen test set.  

---

### Notes

- This is really similar to another idea previously for doing few-shot regression ie. if we hold the feature extractor constant, we can simply solve for the final layer's weights with the given training set
- The authors here train the algorithm on higher-way training tasks, which might be giving similar advantages to other papers that first train the feature extractor on the entire training set of 'base classes'

---

### PS

Paper and code are available [here](http://www.robots.ox.ac.uk/~luca/r2d2.html).
