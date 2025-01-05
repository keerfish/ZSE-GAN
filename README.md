# Visual Enhancement of image stacks from Z-Scanning Microscope using ZSE-GAN
Z-stack scanning captures a series of 2D images for each individual physical tissue section, but these images often suffer from typical blurring effects. The processing data consists of a set of image stacks, as illustrated below.

**Note:** <br />
i. *S_05* to *S_25* are images taken by changing the depth of the focus within the brain slice.<br />
ii. *S_01* to *S_04* are images taken by focusing above the brain slice.<br />
iii. *S_26* to *S_29* are images taken by focusing below the brain slice.<br />
iv. *S_14*, *S_15*, and *S_16* are sharp in-focus images.

<p align="center">
  <img src="https://github.com/keerfish/ZSE-GAN/blob/main/imgs/image_stack.jpg" align="center" width="700px"/>
</p>

Z-stack image enhancement here is inspired by Conditional Generative Adversarial Networks, which was implemented for collection style transfer, object transfiguration, season transfer, photo enhancement, etc. Because the ground truth and the true sharp volumetric image were not available, the classical GAN (e.g., Cycle-Consistent Adversarial Networks shown below) was not a proper method for the image stack enhancement problem. The z-stack image enhancement here formulated the loss and performed the training based on 2D image patches, while the network learned to perform an intensity transformation of volumetric 3D patches.

