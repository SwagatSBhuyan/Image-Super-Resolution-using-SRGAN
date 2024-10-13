# Introduction
![Slide1](https://github.com/user-attachments/assets/783c9743-48a3-4a11-83d9-bf28f0a8936a)
High Resolution (HR) images of their Low Resolution (LR) counterparts is quite an important aspect of many image processing and computer vision applications, such as medical imaging, graphics upscaling, Real time Super Sampling used in video games, graphics rendering, etc.
One very common approach is to upgrade the hardware for the imaging system. But this approach would prove costly and inflexible, not to mention this would only solve the problem of capturing new HR images and not upscale already existent LR images. 
The software based methodology used to convert Low Resolution images into their High Resolution counterparts is called Super Resolution (SR).
It is inherently ill posed since for one LR image, there exists multiple HR ones that could generate it.
*******************************************************************************************************************
# Problem Statement
Development of a robust Generative Adversarial Network for single Image Super Resolution that can generate an upsampled super resolved image from a given low resolution counterpart and development of a custom loss function that is able to capture the finer texture details of the upsampled image and enhance the perceptual quality of the image, rather than
enhancing pixel-wise error, which results in smooth textures.
*******************************************************************************************************************
# Super Resolution
![Slide7](https://github.com/user-attachments/assets/83877494-55d9-4772-864f-9ae55df3e1a2)
![Slide8](https://github.com/user-attachments/assets/701030f8-dc7d-4e2d-a248-107cc60bf124)
*******************************************************************************************************************
# GAN-based approach
We propose a super-resolution GAN for which we employ a deep residual network. More specifically, we will be defining a novel perceptual loss function combined with the discriminator network which will yield solutions hard to distinguish from the HR reference images.
GANs provide a powerful framework for generating plausible-looking natural images with high perceptual quality. The GAN procedure encourages the reconstructions to move towards regions of the search space with high probability of containing photo-realistic images and thus closer to the natural image manifold.
*******************************************************************************************************************


