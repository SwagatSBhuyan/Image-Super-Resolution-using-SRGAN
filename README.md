# Introduction
![Slide1](https://github.com/user-attachments/assets/783c9743-48a3-4a11-83d9-bf28f0a8936a)
High-resolution (HR) images of their low-resolution (LR) counterparts are quite an important aspect of many image processing and computer vision applications, such as medical imaging, graphics upscaling, Real-time Super Sampling used in video games, graphics rendering, etc.
One very common approach is to upgrade the imaging system's hardware. However, this approach would prove costly and inflexible. It would also only solve the problem of capturing new HR images and not upscale already-existent LR images. 
The software-based methodology used to convert Low-Resolution images into their High-Resolution counterparts is called Super Resolution (SR).
It is inherently ill-posed since, for one LR image, there exist multiple HR ones that could generate it.
*******************************************************************************************************************
# Problem Statement
Development of a robust Generative Adversarial Network for Single Image Super Resolution that can generate an upsampled super-resolved image from a given low-resolution counterpart and development of a custom loss function that is able to capture the finer texture details of the upsampled image and enhance the perceptual quality of the image, rather than
enhancing pixel-wise error, which results in smooth textures.
*******************************************************************************************************************
# Super Resolution
![Slide7](https://github.com/user-attachments/assets/83877494-55d9-4772-864f-9ae55df3e1a2)
![Slide8](https://github.com/user-attachments/assets/701030f8-dc7d-4e2d-a248-107cc60bf124)
*******************************************************************************************************************
# GAN-based approach
We propose a super-resolution GAN for which we employ a deep residual network. More specifically, we will define a novel perceptual loss function combined with the discriminator network, which will yield solutions that are hard to distinguish from the HR reference images.
GANs provide a powerful framework for generating plausible-looking natural images with high perceptual quality. The GAN procedure encourages the reconstructions to move towards regions of the search space with a high probability of containing photo-realistic images and, thus, closer to the natural image manifold.
![Slide10](https://github.com/user-attachments/assets/f9166489-7bda-430b-a2c3-e6e887d7fc02)
*******************************************************************************************************************
# Drawbacks of existing methods
> They are not able to recover the finer texture details when we super-resolve at large upscaling factors.
> They focus on minimizing the mean squared error, which is a pixel-wise loss function. 
> Oversimplifies the SR problem and usually yields solutions with overly smooth textures.
> The results have high Peak Signal Noise Ratio (PSNR) values, but they often lack high texture details and fail to capture the patterns.
*******************************************************************************************************************
# Workflow of the proposed methodology
### Workflow Diagram
![Slide13](https://github.com/user-attachments/assets/b6de5709-9aea-41be-85f0-5923d7ae4eab)
### Dataset Folder Recognition
DataLoaders by PyTorch were set up to automatically detect the High-Resolution Images from the Dataset Folder. We used a hybrid dataset for training; we merged the DIV2K, GENERAL100, BSD200, URBAN100, and MANGA109 datasets, standard benchmark datasets for Super Resolution.
We are using a hybrid varied dataset because we want our model to capture the pattern in the images, as this will be necessary for our Generator network. 
### Image Transformations
PyTorch transformations were introduced to make scalable Samples of the images. The various transforms are discussed in the code, but most importantly, the LR and HR transforms were used to fit the images to the required GAN Model Layers. Random Crops are used, where the crop size is calculated from the desired upscaling factor to fit dimensionally into the SRGAN model.
*******************************************************************************************************************
# Model Architecture
The Architecture for the SRGAN was designed as a GAN model. The generator learns to create solutions that are highly similar to real images and, thus, difficult for the discriminator to classify. This encourages perceptually superior solutions residing in natural images' subspace, the manifold. At the core of G, there are residual blocks with identical layouts.
![Slide18](https://github.com/user-attachments/assets/5b5498c1-264f-4bdc-bd35-6bc919c5c5f1)
![Slide19](https://github.com/user-attachments/assets/1d83fa16-4f10-46f1-9885-3f64b3591189)
![Slide20](https://github.com/user-attachments/assets/a2a0f8ee-480c-49b2-95c9-23bab4dcaab8)
![Slide21](https://github.com/user-attachments/assets/52990e57-6c12-40dd-a2b2-24f97fe420b6)
![Slide22](https://github.com/user-attachments/assets/0a82ed1b-ff66-44d6-a7b9-7f9973670db8)
*******************************************************************************************************************
# Training SRGAN model
Several hyperparameters were set, and the necessary loss criteria for the generator and adversarial were introduced.
![image](https://github.com/user-attachments/assets/a03f9f62-777a-4dad-acb4-6456765360f7)
![image](https://github.com/user-attachments/assets/c227789e-9e9b-4fe5-b9aa-0592bf0293f2)
As we can see here, the generator loss network has been assigned, and now, training will begin for 135 epochs with a learning rate of 0.0002. The optimizer used is Adam. Training on Google Colab Pro’s GPU attained a Discriminator loss of 0.001 and a Generator loss of 0.0053. Validation results (20% dataset) were also interesting, as we calculated the various evaluation metrics in runtime here; PSNR: 23.7678 dB SSIM: 0.6503 PI: 3.56
*******************************************************************************************************************
# Evaluation
> **Peak signal-to-noise ratio (PSNR)**: It is the most widely used objective quality assessment metric for image super-resolution. The PSNR is defined as:
![image](https://github.com/user-attachments/assets/6ced298b-39f2-412f-bdf3-fa1953ecc6f0)
> **Drawback**: It is more concerned with the proximity between corresponding pixels, which results in low consistency with perceptual quality and overly smooth textures.
![Slide26](https://github.com/user-attachments/assets/e2b73ecd-5794-412a-95e5-f748b2390324)
![Slide27](https://github.com/user-attachments/assets/fe727422-c0a3-4086-8d3d-752c459ee1d6)
![Slide28](https://github.com/user-attachments/assets/1ea43fdf-ba62-42b1-9656-6038032238e7)
![Slide29](https://github.com/user-attachments/assets/599ef354-86f0-4d68-bef2-3f2dc6c862aa)
![Slide30](https://github.com/user-attachments/assets/299f3001-4031-4b32-ad25-8d41ead468b5)
![Slide31](https://github.com/user-attachments/assets/1f6840a7-2503-4996-bd56-15d5ec63a287)
![Slide32](https://github.com/user-attachments/assets/c066fb94-e0db-4ffa-bc91-53f3ee4da33a)
![Slide33](https://github.com/user-attachments/assets/a9af3120-2434-47b7-aefe-6fe0ade166f7)
![Slide34](https://github.com/user-attachments/assets/f584b0ea-0d45-4a6c-9fe1-c3a95dad2c39)
*******************************************************************************************************************
# Some test results using our model
![Slide37](https://github.com/user-attachments/assets/e36f55d6-8a94-40ad-8fd9-aba570933a4c)
![Slide38](https://github.com/user-attachments/assets/05ad02e7-84a7-4712-aecb-22d53847e33a)
![Slide39](https://github.com/user-attachments/assets/353ffe1c-5e7a-41ec-a228-4e2cb57d4160)
![Slide40](https://github.com/user-attachments/assets/6e81089b-d7b2-44b4-a06b-ed349bd5539f)
*******************************************************************************************************************
# References
[1] C. Dong, C. C. Loy, K. He, and X. Tang, “Learning a deep convolutional network for image super- resolution,” in European conference on computer vision, Springer, Springer, Cham, 2014.
[2] H. Chen, X. He, L. Qing, Y. Wu, C. Ren, R. E. Sheriff, and C. Zhu, “Real-world single image super- resolution: A brief review,” Information Fusion, vol. 79, 2021.
[3] Z. Wang, E. Simoncelli, and A. Bovik, “Multiscale structural similarity for image quality assessment,” in The Thrity-Seventh Asilomar Conference on Signals, Systems Computers, 2003, vol. 2, 2003.
[4] Z. Wang, A. C. Bovik, H. R. Sheikh, and E. P. Simoncelli, “Image quality assessment: from error visibility to structural similarity,” IEEE transactions on image processing, vol. 13, no. 4, 2004.
[5] P. Gupta, P. Srivastava, S. Bhardwaj, and V. Bhateja, “A modified psnr metric based on hvs for quality assessment of color images,” in 2011 International Conference on Communication and Industrial Application, IEEE, 2011.
[6] C. Ledig, L. Theis, F. Huszar, J. Caballero, A. Acosta, A. Aitken, A. Tejani, J. Totz, Z. Wang, and W. Shi, “Photo-realistic single image super-resolution using a generative adversarial network,” 07 2017.
[7] J. Johnson, A. Alahi, and L. Fei-Fei, “Perceptual losses for real-time style transfer and super-resolution,” in European conference on computer vision, Springer, 2016.
[8] J. Bruna, P. Sprechmann, and Y. LeCun, “Super-resolution with deep convolutional sufficient statistics,” arXiv preprint arXiv:1511.05666, 2015.
[9] M. S. Sajjadi, B. Scholkopf, and M. Hirsch, “Enhancenet: Single image super-resolution through automated texture synthesis,” in Proceedings of the IEEE international conference on computer vision, 2017.
[10] I. Goodfellow, J. Pouget-Abadie, M. Mirza, B. Xu, D. Warde-Farley, S. Ozair, A. Courville, and Y. Bengio, “Generative adversarial nets,” Advances in neural information processing systems, vol. 27, 2014.
[11] X. Wang, K. Yu, C. Dong, and C. C. Loy, “Recovering realistic texture in image super-resolution by deep spatial feature transform,” in Proceedings of the IEEE conference on computer vision and pattern recognition, 2018.
[12] K. He, X. Zhang, S. Ren, and J. Sun, “Deep residual learning for image recognition,” in Proceedings of the IEEE conference on computer vision and pattern recognition, 2016.
[13] X. Zhu, L. Zhang, L. Zhang, X. Liu, Y. Shen, and S. Zhao, “Gan-based image super-resolution with a novel quality loss,” Mathematical Problems in Engineering, vol. 2020, 2020.
[14] X. Wang, K. Yu, S. Wu, J. Gu, Y. Liu, C. Dong, Y. Qiao, and C. Change Loy, “Esrgan: Enhanced super-resolution generative adversarial networks,” in Proceedings of the European conference on computer vision (ECCV) workshops, Springer, Cham, 2018.
*******************************************************************************************************************
































