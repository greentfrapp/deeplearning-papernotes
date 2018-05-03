# [Decision-Based Adversarial Attacks: Reliable Attacks Against Black-Box Machine Learning Models](https://arxiv.org/abs/1712.04248)

### Wieland Brendel, Jonas Rauber, Matthias Bethge

#### 16 Feb 2018 `ICLR2018`

--

### Concept

In this paper, the authors introduce the first (AFAIK) truly black-box attack based on just the predicted label from the target classifier. The idea is extremely simple in theory - given two images (e.g. of a Cat and a Dog as classified as the target classifier), we try to move one image as close to the other as possible, **in pixel space**. 

In addition to the black-box decision-based aspect of the attack, the attack also introduces a new paradigm - rather than perturbing a target image, we try to get a source image as close as we can to a target image.

Woops started rambling...

~~Suppose we begin with Cat\_0, we generate Cat\_temp = Cat\_0 + epsilon * (Dog\_0 - Cat\_0). If epsilon = 0, Cat\_temp = Cat\_0 and Cat\_temp is obviously classified as a Cat. If epsilon = 1, Cat\_temp = Dog\_0 and Cat\_temp is obviously classified as a Dog. But there exists an epsilon, such that 0 < epsilon < 1, where Cat\_temp is still classified as a Cat. We can simply start with an arbitrary epsilon. Then we either decrease epsilon and reject Cat\_temp if it is classified as a Dog and try again, or increase epsilon and set Cat\_1 = Cat\_temp if it is classified as a Cat. Assuming epsilon > 0, then MSE(Cat\_1, Dog\_0) < MSE(Cat\_0, Dog\_0).~~

Will rewrite this later.

--

### Notes

- True black-box attack requires minimal info from target classifier
- Requires a ton of predictions to generate a single adversarial image
- Generated adversarial sample seems to be unable to give high confidence since we travel along the decision boundary

--

### Ideas

- Can we reduce the number of predictions required per adversarial sample by reusing the prediction information?
- Is it possible to conduct this attack in feature space and then use an autoencoder / GAN to transform the adversarial features into an image? Will the adversarial characteristics be preserved?
- What if instead of changing all the pixels in the image, we change a random subset of pixels? Is there a good way to pick the subset? Can we also do this for other attacks?
- Can we hide adversarial information in a channel?

--

### PS

They have an implementation in [Foolbox](https://github.com/bethgelab/foolbox).

My reproduced implementation [here](https://github.com/greentfrapp/boundary-attack) for Keras pretrained ResNet50 and a local MNIST classifier.