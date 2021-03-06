# Lapstyle: Laplacian-Steered Neural Style Transfer
Code and test images for the paper "[Laplacian-Steered Neural Style Transfer](https://arxiv.org/abs/1707.01253)".

Lapstyle extends an existing neural style transfer method with one or multiple Laplacian loss layers. The following three neural style transfer implementations have been extended: 

* **lap_style.lua** (*Recommended!*) - https://github.com/jcjohnson/neural-style Gatys-style[1] implemented by Justin Johnson, using the L-BFGS optimization method.
* **tf-neural-style/neural_style.py** - https://github.com/anishathalye/neural-style Gatys-style[1] by Anish Athalye, using Adam. 
* **neural-doodle/doodle.py** - https://github.com/alexjc/neural-doodle MRF-CNN[2] implemented by Alex J. Champandard.

The implementation by Justin Johnson clearly produces the best images (either the original [neural_style.lua](https://github.com/jcjohnson/neural-style/blob/master/neural_style.lua) or the extended [lap_style.lua](https://github.com/askerlee/lapstyle/blob/master/lap_style.lua)). The corresponding content and style losses are also the smallest. Its superiority seems to be ascribed to the L-BFGS optimization, since the algorithm is otherwise identical to Anish Athalye's implementation.

## Setup:
The setup procedures are the same as those of each original project. The following procedures for **lap_style.lua** are quoted from https://github.com/jcjohnson/neural-style:
<blockquote>
Dependencies:
* [torch7](https://github.com/torch/torch7)
* [loadcaffe](https://github.com/szagoruyko/loadcaffe)

Optional dependencies:
* For CUDA backend:
  * CUDA 6.5+
  * [cunn](https://github.com/torch/cunn)
* For cuDNN backend:
  * [cudnn.torch](https://github.com/soumith/cudnn.torch)
* For OpenCL backend:
  * [cltorch](https://github.com/hughperkins/cltorch)
  * [clnn](https://github.com/hughperkins/clnn)

After installing dependencies, you'll need to run the following script to download the VGG model:
```
sh models/download_models.sh
```
This will download the original [VGG-19 model](https://gist.github.com/ksimonyan/3785162f95cd2d5fee77#file-readme-md).
</blockquote>

### Sample usage:
```
th lap_style.lua -style_image images/flowers.png -content_image images/megan.png -output_image output/megan_flowers20_100.png -content_weight 20 -lap_layers 2 -lap_weights 100
```

### Sample images:
<p align='center'>
  <img src='images/megan.png' width='400'/>
  <img src='images/flowers.png' width='400'/><br>
  <img src='output/megan_flowers20_0.png' width='400'/>
  <img src='output/megan_flowers20_100.png' width='400'/>  
</p>
<p align='center'>
  <img src='images/girlmrf.jpg' width='300'/>
  <img src='images/smallworldI.jpg' width='300'/><br>
  <img src='output/girlmrf_smallworldI_20_0.png' width='300'/>
  <img src='output/girlmrf_smallworldI_20_200.png' width='300'/>  
</p>

The four images in each group are: 1) content image, 2) style image, 3) image synthesized with the original Gatys-style, and 4) image synthesized with Lapstyle.

Note: although photo-realistic style transfer[3] (https://github.com/luanfujun/deep-photo-styletransfer) performs amazingly well on their test images, it doesn't work on the images we tested. Seems that in order to make it work well, the content image and the style image has to have highly similar layout and semantic contents.

### Citation
You are welcome to cite the paper (https://arxiv.org/abs/1707.01253) with this bibtex:

```
@InProceedings{lapstyle,
  author    = {Shaohua Li and Xinxing Xu and Liqiang Nie and Tat-Seng Chua},
  title     = {Laplacian-Steered Neural Style Transfer},
  booktitle = {Proceedings of the ACM Multimedia Conference (MM), to appear.},
  year      = {2017},
}
```

### References
[1] Leon A Gatys, Alexander S Ecker,and Matthias Bethge. 2016. Image style transfer using convolutional neural networks. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2414–2423.

[2] Chuan Li and Michael Wand. 2016. Combining markov random fields and convolutional neural networks for image synthesis. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2479–2486.

[3] Fujun Luan, Sylvain Paris, Eli Shechtman, and Kavita Bala. 2017. Deep Photo Style Transfer. arXiv preprint arXiv:1703.07511 (2017).
