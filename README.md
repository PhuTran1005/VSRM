# [ICCV 2025] VSRM
[ICCV 2025] Official repository for "VSRM: A Robust Mamba-Based Framework for Video Super-Resolution"

### VSRM: A Robust Mamba-Based Framework for Video Super-Resolution [[Paper Link]](https://openaccess.thecvf.com/content/ICCV2025/papers/Tran_VSRM_A_Robust_Mamba-Based_Framework_for_Video_Super-Resolution_ICCV_2025_paper.pdf)
[Dinh Phu Tran](https://scholar.google.com/citations?user=peeXHDYAAAAJ&hl=en), [Dao Duy Hung](https://github.com/PhuTran1005/VSRM), and [Daeyoung Kim](https://github.com/PhuTran1005/VSRM)

[![arXiv](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2506.22762)
![visitors](https://visitor-badge.laobi.icu/badge?page_id=PhuTran1005.VSRM)
[![GitHub Stars](https://img.shields.io/github/stars/PhuTran1005/SAT?style=social)](https://github.com/PhuTran1005/VSRM)

## Updates
- 🎉 2025-06-25: Accepted to ICCV 2025!
- ✅ 2026-04-05: Release repository

## Overview

**Abstract:**

> Video super-resolution remains a major challenge in low-level vision tasks.
To date, CNN- and Transformer-based methods have delivered impressive results. However, CNNs are limited by local receptive fields, while Transformers struggle with quadratic complexity, posing challenges for processing long sequences in VSR. Recently, Mamba has drawn attention for its long-sequence modeling, linear complexity, and large receptive fields. In this work, we propose VSRM, a novel **V**ideo **S**uper-**R**esolution framework that leverages the power of **M**amba. VSRM introduces Spatial-to-Temporal Mamba and Temporal-to-Spatial Mamba blocks to extract long-range spatio-temporal features and enhance receptive fields efficiently. To better align adjacent frames, we propose Deformable Cross-Mamba Alignment module. This module utilizes a deformable cross-mamba mechanism to make the compensation stage more dynamic and flexible, preventing feature distortions. Finally, we minimize the frequency domain gaps between reconstructed and ground-truth frames by proposing a simple yet effective Frequency Charbonnier-like loss that better preserves high-frequency content and enhances visual quality. Through extensive experiments, VSRM achieves state-of-the-art results on diverse benchmarks, establishing itself as a solid foundation for future research.

**Overall Architecture of VSRM:**

<img src="https://raw.githubusercontent.com/PhuTran1005/VSRM/master/figures/overall_architecture.png" width="600"/>

#### Structure and scan directions of Mamba modules:

<img src="https://raw.githubusercontent.com/PhuTran1005/VSRM/master/figures/direction_scan.png" width="300"/>

#### Temporal Gated Feed-forward Network

<img src="https://raw.githubusercontent.com/PhuTran1005/VSRM/master/figures/tgfn.png" width="300"/>

**Quantitative Results:**

<img src="https://raw.githubusercontent.com/PhuTran1005/VSRM/master/figures/performance.png" width="600"/>

**Qualitative Results:**

<img src="https://raw.githubusercontent.com/PhuTran1005/VSRM/master/figures/vis.png" width="600"/>

## Environment
- [PyTorch >= 1.1.1](https://pytorch.org/) **(Recommend **NOT** using torch 1.8!!! It would cause abnormal performance.)**
- [BasicSR == 1.3.4.9](https://github.com/XPixelGroup/BasicSR/blob/master/INSTALL.md)
### Installation
Install Pytorch first.
Then,
```
pip install -r requirements.txt
python setup.py develop
```

## How To Test

- Run the following codes:
```
# For model trained on REDS dataset with BI degradation. 
python test_scripts/BI/REDS/test_VSRM_REDS4_N6.py
python test_scripts/BI/REDS/test_VSRM_REDS4_N16.py
python test_scripts/BI/REDS/test_VSRM_Vid4_N6.py
python test_scripts/BI/REDS/test_VSRM_Vid4_N16.py

# For model trained on Vimeo-90K dataset with BI degradation. 
python test_scripts/BI/Vimeo-90K/test_VSRM_Vid4.py
python test_scripts/BI/Vimeo-90K/test_VSRM_Vimeo-90K-T.py
```
The testing results will be saved in the `./results` folder.

## How To Train

- Refer to `./options/train` for the configuration file of the model to train.
- Preparation of training data can refer to [this page](https://github.com/XPixelGroup/BasicSR/blob/master/docs/DatasetPreparation.md).

- The training command is like
```
# VSR trained on REDS with 6 input frames, tested on REDS4
bash dist_train.sh 8 options/SRM_REDS_N6_300K.yml

# VSR trained on REDS with 16 input frames, tested on REDS4
bash dist_train.sh 8 options/VSRM_REDS_N16_600K.yml
```

The training logs and weights will be saved in the `./experiments` folder.

Due to the incompatibility of pytorch checkpoint and distributed training, the training process will terminate after the first 5000 iterations. To resume the training, execute the training script again and the previously saved parameters will be automatically loaded. This will restore the normal training procedure.

## Citations
#### BibTeX

```
@inproceedings{tran2025vsrm,
  title={VSRM: A Robust Mamba-Based Framework for Video Super-Resolution},
  author={Tran, Dinh Phu and Hung, Dao Duy and Kim, Daeyoung},
  booktitle={Proceedings of the IEEE/CVF International Conference on Computer Vision},
  pages={14711--14721},
  year={2025}
}
```

## Acknowledgement

Our codes was built on [BasicSR](https://github.com/xpixelgroup/basicsr) and [PSRT](https://github.com/XPixelGroup/RethinkVSRAlignment). Thank you authors for sharing their great works.