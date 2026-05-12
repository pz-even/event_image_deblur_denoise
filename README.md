# Neuromorphic Imaging with Joint Image Deblurring and Event Denoising</h1>

[![doi](https://img.shields.io/badge/Journal-IEEE_TIP-blue)](https://doi.org/10.1109/TIP.2024.3374074)
[![arXiv](https://img.shields.io/badge/arXiv-PDF-b31b1b)](https://arxiv.org/abs/2309.16106)
[![HKU](https://img.shields.io/badge/HKU-PDF-b31b1b)](https://www.eee.hku.hk/optima/pub/journal/2403_ITIP.pdf)
[![Dataset](https://img.shields.io/badge/Dataset-Available-00b894)](https://bora.teracloud.jp/share/12224f5298482b21)
![MATLAB](https://img.shields.io/badge/MATLAB-R2021a-e16737)
![License](https://img.shields.io/badge/License-MIT-green)
[![News](https://img.shields.io/badge/News-计思光益-07C160)](https://mp.weixin.qq.com/s/TB-1bdcrLdd-AZwZ_iZWAg)

```
@article{zhang2024tip,
  title    =  {Neuromorphic Imaging with Joint Image Deblurring and Event Denoising},
  author   =  {Pei Zhang and Haosen Liu and Zhou Ge and Chutian Wang and Edmund Y. Lam},
  journal  =  {IEEE Transactions on Image Processing},
  volume   =  {33},
  pages    =  {2318--2333},
  month    =  {March},
  year     =  {2024},
  doi      =  {10.1109/TIP.2024.3374074},
}
```
![DEMO](./imgs/demo.png)
![DEMO](./imgs/demo2.png)

## Implementation
Before start, take a look at the uploaded good and failed samples in the `data` and `results` folders.
### Preparation
1. Put your image file and its event data in the folder set by `configs.data` in `demo.m` (default: `data`).
2. The event data must be in `.mat` and with `t, x, y, p` entries.

### Run
Run `demo.m` with the following configurations:
```
configs.dir:              dir name
configs.data:             folder to store input data
configs.results:          folder to store output results
configs.blur:             input image file
configs.evs:              input event file
configs.dvs_resolution:   DVS spatial resolution
configs.alpha:            weight of the event regularizer
configs.beta:             weight of the l_0 regularizer
configs.sigma:            weight of the Gaussian regularizer
configs.weight:           weight of gradient supervision
configs.N:                find neighbors (1) or not (0)
configs.dx:               spatial threshold to set a square neighborhood boundary
configs.dt:               temporal threshold to set a neighborhood boundary
configs.case:             set a use case (-1, 1, 2)
```
For convenience, we split our algorithm into 3 functions, controlled by `configs.case`:
1. `configs.case = -1` for joint image deblurring and event denoising.
2. `configs.case = 1` for image deblurring only (if you have a blurry image and clean events). These configurations are disabled (any value): `configs.weight`, `configs.N`, `configs.dx`, `configs.dt`.
3. `configs.case = 2` for event denoising only (if you have a sharp image and noisy events). These configurations are disabled (any value): `configs.alpha`, `configs.beta`, `configs.sigma`.

### Result
These files will be generated in the folder set by `configs.results` in `demo.m` (default: `results`):
1. `xxx_configs.mat` for configurations used.
2. `xxx_sharp.png` for a restored sharp image (only for `configs.case = -1` and `configs.case = 1`).
3. `xxx_kernel.png` for an estimated blur kernel (only for `configs.case = -1` and `configs.case = 1`).
4. `xxx_signals.mat` for denoised events (only for `configs.case = -1` and `configs.case = 2`).

## Dataset
![DATA](./imgs/data.png)
Real-world pairs of blurry images and noisy event streams, captured by a DAVIS346 camera on a rich range of scenarios. Download it from [here](https://bora.teracloud.jp/share/12224f5298482b21).
