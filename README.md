# Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation [WACV 2025]
This repository is the official implementation of "Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation", accepted to WACV 2025.

## Abstract
Weakly-supervised Semantic Segmentation (WSSS) aims to provide a precise semantic segmentation results without expensive pixel-wise segmentation labels.
With the supervision gap between classification and segmentation, Image-level WSSS mainly relies on Class Activation Maps (CAMs) from the classification model to emulate the pixel-wise annotations.
However, CAMs often fail to cover the entire object region because classification models tend to focus on narrow discriminative regions in an object.
Towards accurate CAM coverage, Existing WSSS methods have tried to boost feature representation learning or impose consistency regularization to the classification models, but still there are limitation in activating non-discriminative area, where the focus of the models is weak.
To tackle this issue, we propose FSAE framework, which provides explicit supervision of non-discriminative area, encouraging the CAMs to activate on various object features.
We leverage weak-strong consistency with pseudo-label expansion strategy for reliable supervision and enhance learning of non-discriminative object boundaries.
Specifically, we use strong perturbation to make challenging inference target, and focus on generating reliable pixel-wise supervision signal for broad object regions.
Extensive experiments on the WSSS benchmark datasets show that our method boosts initial seed quality and segmentation performance by large margin, achieving new state-of-the-art performance on benchmark WSSS datasets.

# Setting up
We followed each base models' environment settings. For exact instructions, please refer to:

- PPC: [https://github.com/usr922/wseg]
- SIPE: [https://github.com/chenqi1126/sipe]
- MCTFormer: [https://github.com/xulianuwa/MCTformer]

or navigate the forked branches in this repository.

## Environments
Our method is tested on single NVIDIA RTX 3090 with CUDA 11.7, Ubuntu 18.04.


- Python 3.8.5
- Pytorch 1.11 or higher
- Pydensecrf from https://github.com/lucasb-eyer/pydensecrf
- opencv-python

## Datasets (WIP)
<details>
<summary>
PASCAL VOC 2012
</summary>

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

  </details>

<details>
<summary>
MS COCO 2014
</summary>

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

  </details>

# Performance (WIP)
- PASCAL VOC 2012
| basemodel      | train mIoU  | val mIoU  | test mIoU   |
| --------       | ----------- | :---------: | :-------: | 
| PPC+Ours       | X           |    61.5     |   58.4    | 
| MCTFormer+Ours | O           |    70.5     |     -     |
| SIPE+Ours      | X           |      -      |   72.3*   |

- COCO 2014
