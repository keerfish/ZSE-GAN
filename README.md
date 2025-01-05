# Visual Enhancement of image stacks from Z-Scanning Microscope using ZSE-GAN
Z-stack scanning captures a series of 2D images for each individual physical tissue section, but these images often suffer from typical blurring effects. The processing data consists of a set of image stacks, as illustrated below.

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/stack_view.jpg" align="center" width="450px"/>
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/image_stack.jpg" align="center" width="450px"/>
</p>

**Note:** <br />
*S_05* to *S_25* are images taken by changing the depth of the focus within the brain slice.<br />
*S_01* to *S_04* are images taken by focusing above the brain slice.<br />
*S_26* to *S_29* are images taken by focusing below the brain slice.<br />
*S_14*, *S_15*, and *S_16* are sharp in-focus images.

Z-stack image enhancement here is inspired by Conditional Generative Adversarial Networks[[1]](#1), which was implemented for collection style transfer, object transfiguration, season transfer, photo enhancement, etc. Because the ground truth and the true sharp volumetric image were not available, the classical GAN (e.g., Cycle-Consistent Adversarial Networks[[2]](#2) shown below) was not a proper method for the image stack enhancement problem. The z-stack image enhancement here formulated the loss and performed the training based on 2D image patches, while the network learned to perform an intensity transformation of volumetric 3D patches.

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/architecture_CNN.jpg" align="center" width="500px"/>
</p>

## ZSE-GAN (Z-Stack Enhancement GAN)
The goal is to translate an image stack sample $x$ from an image set of z-scan stacks to the desired sharp
volumetric image $y$. The cross-sections of $y$ have a sharpness similar to that of the in-focus image. The model
includes two 3D translators $G_S$ and $G_B$, as well as two 2D discriminators, $D_S$ and $D_B$. The horizontal cross-sectional image of an image stack sample $x$ is denoted by $x_{\Vert}$. The horizontal and vertical cross-sectional images of an image stack sample $y$ are denoted by $y_{\Vert}$ and $y_{\perp}$, as well as those of a transformed sample $G_B(y)$ are denoted by $`G_B(y)_{\Vert}`$ and $`G_B(y)_{\perp}`$. $D_B$ aims to differentiate between images
$x_{\Vert}$ and $`G_B(y)_{\Vert}`$, whereas $D_S$ works analogously for the images $y_{\Vert}$, $y_{\perp}$ and image $`y^*`$ , where $`y^*`$ is drawn from the 2D in-focus images scanned from the focal plane. The architecture of the ZSE-GAN network is illustrated below. 

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/semi_architecture.jpg" align="center" width="500px"/>
</p>

## Visual Results

The textural properties of the vertical cross-sections and horizontal sections of the output z-stack are indistinguishable from those of the horizontal sections close to the center of the input stack. The cellular structures are overall consistent.

### Input Image Stack
Cross sections of an input image stack $x$:
<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/cross_x.jpg" align="center" width="500px"/>
</p>

### Output Image Volume
Cross sections of the corresponding output volumetric image $G_S(x)$:
<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/cross_y.jpg" align="center" width="500px"/>
</p>

The ZSE-GAN modifies image intensities of the z-stack such that the textural properties of the vertical cross-sections and horizontal
sections near the top and bottom of the output z-stack are indistinguishable from those of the horizontal sections
close to the center of the input stack. At the same time, the output does not introduce new cellular structures.

## Important Information
For a detailed explanation of the principles and implementation, please refer to the [ZSE GAN](https://github.com/keerfish/ZSE-GAN/blob/main/ZSE_GAN.pdf). This method was developed in collaboration with my colleagues Timo Dickscheid and Eric Upschult as part of a submission created three years ago. The well-crafted and professional introduction was written by Timo, while Eric provided valuable support for the idea and discussions. I completed the remaining sections and the coding. Ultimately, I persuaded Timo and Eric not to submit the paper, as I was dissatisfied with the quantitative analysis, which lacked clear, strong, and solid theoretical support. 

## Acknowledgments
The code is heavily adopted from [pix2pix](https://github.com/phillipi/pix2pix), and [DCGAN](https://github.com/soumith/dcgan.torch). The idea of ZSE-GAN is inspired by [CycleGAN](https://github.com/junyanz/CycleGAN/tree/master).

## References
<a id="1">[1]</a>
Mehdi Mirza and Simon Osindero. 
Conditional Generative Adversarial Nets. 
ArXiv, 
Volume abs/1411.1784, 
2014.

<a id="2">[2]</a>
Zhu, Jun-Yan and Park, Taesung and Isola, Phillip and Efros, Alexei A. 
Unpaired Image-to-Image Translation Using Cycle-Consistent Adversarial Networks. 
IEEE International Conference on Computer Vision (ICCV)}, 
pages 2242-2251,
2017.



