## [Attentive Image Deraining Network with Better Generalization]

### Introduction
In recent years, single image deraining has received considerable progress based on deep learning.
However, existing deep deraining networks are usually facing the problems of either over-smoothing background
images or inadequate removing rain streaks, especially when applying to real-world rainy images. In this paper,
we try to tackle this issue from two perspectives. First, in terms of network architecture, we propose an attentive
image deraining network (AIDNet), where residual attention block is proposed to exploit the beneficial deep features
from the rain streak layer to the background image layer. Second, we propose to adopt pixel-shuffle downsampling (PSD)
as a simple pre-processing step to improve the generalization ability of AIDNet, where the severe rain streaks
in real-world rainy images can be well relieved. Moreover, the PSD operation can be applied to other deep deraining
networks to boost their deraining performance. Experimental results on both synthetic datasets and real-world rainy
images demonstrate that our AIDNet notably outperforms state-of-the-art deep deraining models.

## Prerequisites
- Python 3.6, PyTorch >= 1.0.0
- Requirements: opencv-python, tensorboardX
- Platforms: Ubuntu 16.04, cuda-10.0 & cuDNN v-7.6.0
- MATLAB for computing [evaluation metrics](statistic/)

## Datasets
PRN and PReNet are evaluated on five datasets*:
Rain100H [1], Rain100L [1], Rain12 [2] , SPAData [4].
Please download the testing datasets from [BaiduYun](https://pan.baidu.com/s/1vK5OfNvPAdGlnvu_e1KeKw, extraction code : aid5)
and place the unzipped folders into `./datasets/test/`.

To train the models, please download training datasets:
RainTrainH [1], RainTrainL [1], RainHeavy [3] and RainLight [3] from [BaiduYun](https://pan.baidu.com/s/1vK5OfNvPAdGlnvu_e1KeKw extraction code : aid5)
and place the unzipped folders into `./datasets/train/`.

## Getting Started

### 1) Testing

We have placed our pre-trained models into `./logs/`.

Run shell scripts to train the models:
python test_AID.py
python test_AID_real.py
python test_AID_simple_real.py

### 2) Evaluation metrics

We also provide the MATLAB scripts to compute the average PSNR and SSIM values reported in the paper.

```Matlab
 cd ./statistic
 run statistic_Rain100H.m
 run statistic_Rain100L.m
 run statistic_Rain12.m
 run statistic_real.m
 run statistic_Ablation.m  # compute the metrics in Ablation Study
```
###
Average PSNR/SSIM values on four datasets:

Dataset    |GMM        |DDN        |SIRR       |JORDER     |BRN        |PReNet     |AIDNet     |
-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
Rain100H   |15.05/0.425|21.92/0.764|22.47/0.716|26.54/0.835|30.47/0.913|29.46/0.899|31.21/0.921|
Rain100L   |28.66/0.865|32.16/0.936|32.37/0.926|36.61/0.974|38.16/0.982|37.48/0.979|40.41/0.988|
Rain12     |32.02/0.855|31.78/0.900|34.02/0.935|33.92/0.953|36.74/0.959|36.66/0.961|37.08/0.973|

Dataset    |DDN        |RESCAN     |SIRR       |SPANet     |PReNet     |JORDER-E   |BRN        |AIDNet     |
-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
SPA_NO_PD  |34.80/0.936|34.86/0.935|34.84/0.936|35.24/0.944|35.00/0.941|33.78/0.931|34.91/0.939|34.97/0.941|
SPA_PD     |34.83/0.940|35.45/0.943|34.93/0.941|35.22/0.945|35.31/0.946|34.23/0.938|35.34/0.945|35.43/0.949|

### 3) Training

Run shell scripts to train the models:
python train_Heavy_aid135.py
python train_Light_aid135.py

## References
[1] Yang W, Tan RT, Feng J, Liu J, Guo Z, Yan S. Deep joint rain detection and removal from a single image. In IEEE CVPR 2017.

[2] Li Y, Tan RT, Guo X, Lu J, Brown MS. Rain streak removal using layer priors. In IEEE CVPR 2016.

[3] W Yang, RT Tan, J Feng, Z Guo, S Yan and J Liu. Joint Rain Detection and Removal from a Single Image with Contextualized Deep Networks. In IEEE TPAMI 2020.

[4] T Wang, X Yang, K Xu, S Chen, Q Zhang, and RWH Lau. Spatial Attentive Single-Image Deraining With a High Quality Real Rain Dataset. In IEEE CVPR 2019.

