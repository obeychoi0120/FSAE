# Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation [WACV 2025]
This is the official implementation of "Feature-level and Spatial-level Activation Expansion for Weakly-Supervised Semantic Segmentation".

## Abstract
Weakly-supervised Semantic Segmentation (WSSS) aims to provide a precise semantic segmentation results without expensive pixel-wise segmentation labels.
With the supervision gap between classification and segmentation, Image-level WSSS mainly relies on Class Activation Maps (CAMs) from the classification model to emulate the pixel-wise annotations.
However, CAMs often fail to cover the entire object region because classification models tend to focus on narrow discriminative regions in an object.
Towards accurate CAM coverage, Existing WSSS methods have tried to boost feature representation learning or impose consistency regularization to the classification models, but still there are limitation in activating non-discriminative area, where the focus of the models is weak.
To tackle this issue, we propose FSAE framework, which provides explicit supervision of non-discriminative area, encouraging the CAMs to activate on various object features.
We leverage weak-strong consistency with pseudo-label expansion strategy for reliable supervision and enhance learning of non-discriminative object boundaries.
Specifically, we use strong perturbation to make challenging inference target, and focus on generating reliable pixel-wise supervision signal for broad object regions.
Extensive experiments on the WSSS benchmark datasets show that our method boosts initial seed quality and segmentation performance by large margin, achieving new state-of-the-art performance on benchmark WSSS datasets.

# Setting up FSAE
## Environments
Our method is tested on single NVIDIA RTX 3090 with CUDA 11.7, Ubuntu 18.04.
We followed each base models' environment settings. For detailed instructions, please refer to:
PPC: [https://github.com/usr922/wseg]
SIPE: [https://github.com/chenqi1126/sipe]
MCTFormer: [https://github.com/xulianuwa/MCTformer]
- Python 3.8.5
- Pytorch 1.11 or higher
- Pydensecrf from https://github.com/lucasb-eyer/pydensecrf
- opencv-python
