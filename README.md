# Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation [WACV 2025]
This repository is the official implementation of "Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation", accepted to WACV 2025.

### Abstract
Weakly-supervised Semantic Segmentation (WSSS) aims to provide a precise semantic segmentation results without expensive pixel-wise segmentation labels.
With the supervision gap between classification and segmentation, Image-level WSSS mainly relies on Class Activation Maps (CAMs) from the classification model to emulate the pixel-wise annotations.
However, CAMs often fail to cover the entire object region because classification models tend to focus on narrow discriminative regions in an object.
Towards accurate CAM coverage, Existing WSSS methods have tried to boost feature representation learning or impose consistency regularization to the classification models, but still there are limitation in activating non-discriminative area, where the focus of the models is weak.
To tackle this issue, we propose FSAE framework, which provides explicit supervision of non-discriminative area, encouraging the CAMs to activate on various object features.
We leverage weak-strong consistency with pseudo-label expansion strategy for reliable supervision and enhance learning of non-discriminative object boundaries.
Specifically, we use strong perturbation to make challenging inference target, and focus on generating reliable pixel-wise supervision signal for broad object regions.
Extensive experiments on the WSSS benchmark datasets show that our method boosts initial seed quality and segmentation performance by large margin, achieving new state-of-the-art performance on benchmark WSSS datasets.

# Setup (WIP)
## Environments
Our method is tested on single NVIDIA RTX 3090 with CUDA 11.7, Ubuntu 18.04. Essential packages are as below:
- Python 3.8.8 or higher
- Pytorch 1.7.1 or higher
- Pydensecrf from https://github.com/lucasb-eyer/pydensecrf
- opencv-python
  
For maximum reproducibility, We recommend to construct individual virtualenv for each base model from the forked branches in this repos

or follow the details from original repos:

- [PPC](https://github.com/usr922/wseg)
- [SIPE](https://github.com/chenqi1126/sipe)
- [MCTFormer](https://github.com/xulianuwa/MCTformer)

  
## Datasets (WIP)
### PASCAL VOC 2012
- Download PASCAL VOC 2012 from this [link](http://host.robots.ox.ac.uk/pascal/VOC/voc2012).
  ``` bash
  wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
  tar –xvf VOCtrainval_11-May-2012.tar
  ```
- Download augmented training set `SegmentationClassAug.zip` from [SBD dataset](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6126343&casa_token=cOQGLW2KWqUAAAAA:Z-QHpQPf8Pnb07A75yBm2muYjqJwYUYPFbwwxMFHRcjRX0zl45kEGNqyTEPH7irB2QbabZbn&tag=1) from this [link](https://www.dropbox.com/s/oeu149j8qtbs1x0/SegmentationClassAug.zip?dl=0).
- The directories should be like below:
  ``` bash
  ├── VOCdevkit/
  │    └── VOC2012
  │     ├── Annotations
  │     ├── ImageSets
  │     ├── JPEGImages
  │     ├── SegmentationClass
  │     ├── SegmentationClassAug
  │     └── SegmentationObject
    ```
### MS COCO 2014
- Download [MS COCO 2014 dataset](https://cocodataset.org/#home)
  ``` bash
  wget http://images.cocodataset.org/zips/train2014.zip
  wget http://images.cocodataset.org/zips/val2014.zip
  ```
- The directories should be like below:
  ``` bash
  ├── COCO2014/
  │   ├── train/              
  │   │   ├── image/     
  │   │   ├── mask/        
  │   │   └── xml/
  │   └── validation/
  │       ├── image/     
  │       ├── mask/        
  │       └── xml/
  ```
# Usage
Please navigate the other branches.

# Performance
Marked with * means reproduced performance.
- PASCAL VOC 2012

  | basemodel      | Mask mIoU  | val mIoU   | test mIoU  | 
  | -------------  | :--------: | :--------: | :--------: | 
  | [PPC](https://github.com/usr922/wseg)            |    73.3    |    74.4    |   75.0     | 
  | **PPC+Ours**       |    **77.0**    |    **74.4**    |   **75.0**     | 
  | [SIPE](https://github.com/chenqi1126/sipe)           |    64.7    |    68.8    |   73.6     | 
  | **SIPE+Ours**      |    **70.5**    |    **69.9**    |   **71.2**     | 
  | [MCTFormer](https://github.com/xulianuwa/MCTformer)*      |    67.9    |    69.0    |   69.8     | 
  | **MCTFormer+Ours** |    **68.8**    |    **69.8**    |   **70.5**     | 

- COCO 2014

  | basemodel      |  val mIoU  | 
  | -------------  | :--------: |
  | PPC*           |    33.7    |
  | PPC+Ours       |    35.4    |
  | SIPE           |    39.3    |
  | SIPE+Ours      |    39.5    |
