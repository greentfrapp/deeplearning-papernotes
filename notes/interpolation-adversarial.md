# [Understand and Improving Interpolation in Autoencoders via an Adversarial Regularizer](https://arxiv.org/abs/1807.07543)

### David Berthelot, Colin Raffel, Aurko Roy, Ian Goodfellow

#### 19 Jul 2018

---

### Concept

This paper introduces an interesting take on the adversarial theme in GANs. 

Specifically, an autoencoder attempts to generate an image using an interpolation of the latent vectors from two images. The discriminator uses the generated image to guess the degree of interpolation. The goal here is to get the autoencoder to generate a realistic interpolated image and so its goal here is to fool the discriminator to predicting that the image has zero interpolation ie. it is a real image.



---

### Notes

- To stabilize the training, the authors use a form of regularization (see Equation 1) such that the discriminator is exposed to realistic data even with poor autoencoder reconstruction and trains it to output 0 for real images

---

### Ideas

- More generally, we might be able to extend this to other applications by understanding the concept as using a latent variable in the data generation process and for the discriminator to try to detect the latent variable used.

---

### PS

Authors' implementation available [here](https://github.com/brain-research/acai).
