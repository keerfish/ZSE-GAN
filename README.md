# Visual Enhancement of image stacks from Z-Scanning Microscope using ZSE-GAN
Z-stack scanning captures a series of 2D images for each individual physical tissue section, but these images often suffer from typical blurring effects. The processing data consists of a set of image stacks, as illustrated below.

**Note:** <br />
*S_05* to *S_25* are images taken by changing the depth of the focus within the brain slice.<br />
*S_01* to *S_04* are images taken by focusing above the brain slice.<br />
*S_26* to *S_29* are images taken by focusing below the brain slice.<br />
*S_14*, *S_15*, and *S_16* are sharp in-focus images.

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/image_stack.jpg" align="center" width="550px"/>
</p>

Z-stack image enhancement here is inspired by Conditional Generative Adversarial Networks, which was implemented for collection style transfer, object transfiguration, season transfer, photo enhancement, etc. Because the ground truth and the true sharp volumetric image were not available, the classical GAN (e.g., Cycle-Consistent Adversarial Networks shown below) was not a proper method for the image stack enhancement problem. The z-stack image enhancement here formulated the loss and performed the training based on 2D image patches, while the network learned to perform an intensity transformation of volumetric 3D patches.

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/architecture_CNN.jpg" align="center" width="550px"/>
</p>

## ZSE-GAN (Z-Stack Enhancement GAN)
The goal is to translate an image stack sample $x$ from an image set of z-scan stacks to the desired sharp
volumetric image $y$. The cross-sections of $y$ have a sharpness similar to that of the in-focus image. The model
includes two 3D translators $G_S$ and $G_B$, as well as two 2D discriminators, $D_S$ and $D_B$. The horizontal cross-sectional image of an image stack sample $x$ is denoted by $x_{\Vert}$. The horizontal and vertical cross-sectional images of an image stack sample $y$ are denoted by $y_{\Vert}$ and $y_{\perp}$, as well as those of a transformed sample $G_B(y)$ are denoted by $`G_B(y)_{\Vert}`$ and $`G_B(y)_{\perp}`$. $D_B$ aims to differentiate between images
$x_{\Vert}$ and $`G_B(y)_{\Vert}`$, whereas $D_S$ works analogously for the images $y_{\Vert}$, $y_{\perp}$ and image $`y^*`$ , where $`y^*`$ is drawn from the 2D in-focus images scanned from the focal plane. The architecture of the ZSE-GAN network is illustrated below. 


