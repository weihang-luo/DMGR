# Dual-Manifold Gradient Rectification (DMGR)

## Overview

This repository contains the official implementation of **"Dual-Manifold Gradient Rectification: Reconciling Topology and Texture in Industrial Anomaly Synthesis"**, published in **IEEE Access** [1].

### Key Contributions

- **Dual-Manifold Gradient Rectification (DMGR)**: We reformulate defect synthesis as a deterministic trajectory rectification process. Unlike heuristic blending, DMGR explicitly models the interaction between a **Base Structural Field** (Global Manifold) and a **Rectification Field** (Local Defect Manifold) to reconcile global topology with local defect fidelity.
- **Physics-Grounded Spectral-Spatial Alignment**: To ensure physical plausibility, we introduce a mechanism that dynamically injects high-frequency defect details. This involves a **Dynamic Multi-Scale Loss** for spectral consistency and an **Uncertainty-Adaptive Spatial Gating** strategy that regulates the rectification region based on generative uncertainty.
- **Asymmetric Collaborative Evolution**: A dynamic scheduling strategy coordinates the interaction between **Structural Anchoring** (early stage) and **Textural Resonance** (late stage). This effectively harmonizes global topology with local defect fidelity by adjusting the rectification strength along the diffusion trajectory 

## Installation

- Python 3.8+ recommended
- PyTorch (CUDA recommended). Install the version matching your CUDA.
- Other Python packages: numpy, pyyaml, pillow, matplotlib

## Model Checkpoints

### Pre-trained Models

To reproduce the results on the PCB dataset mentioned in the paper, please download the following pre-trained models and place them in the `checkpoint/` directory.

**Note**: The Global Model was trained on 256x256 defect-free images, and the Local Model was trained on 64x64 defect patches [283, 285].

#### 1. Global Context Model (global-256.pt)

This model establishes the Base Structural Field (Global Manifold).

- **Filename**: `global-256.pt`
- **Download Link**: [Download from Google Drive](https://drive.google.com/uc?export=download&id=1axJMm0fpg0v2HIApxz0IIaY0WTDKalCH)

```bash
wget -O checkpoint/global-256.pt "[https://drive.google.com/uc?export=download&id=1axJMm0fpg0v2HIApxz0IIaY0WTDKalCH](https://drive.google.com/uc?export=download&id=1axJMm0fpg0v2HIApxz0IIaY0WTDKalCH)"
````

#### 2\. Defect Patch Model (defect-patch-64.pt)

This model provides the Rectification Field (Local Defect Manifold).

  - **Filename**: `defect-patch-64.pt`
  - **Download Link**: [Download from Google Drive](https://drive.google.com/uc?export=download&id=1GHT-q1XjF_aCmInp_g5gMruX3yih-iyM)

<!-- end list -->

```bash
wget -O checkpoint/defect-patch-64.pt "[https://drive.google.com/uc?export=download&id=1GHT-q1XjF_aCmInp_g5gMruX3yih-iyM](https://drive.google.com/uc?export=download&id=1GHT-q1XjF_aCmInp_g5gMruX3yih-iyM)"
```

### Directory Structure After Setup

```bash
checkpoint/
├── global-256.pt          # Global context model (Base Structural Field)
└── defect-patch-64.pt     # Local defect patch model (Rectification Source)
```

## Quick start

1)  Verify checkpoints are in `checkpoint/`.
2)  Use the provided config `confs/pcb_gen.yml`.
3)  Run synthesis:

<!-- end list -->

```bash
python Gen.py --conf_path confs/pcb_gen.yml
```

Outputs will be saved under `images/fj_ddim/`:

  - `images/fj_ddim/samples/`: generated samples
  - `images/fj_ddim/gird/`: grids of intermediate predictions
  - `images/fj_ddim/crop/`: defect patch crops

### Configuration

The main configuration file is `confs/pcb_gen.yml`. Parameters related to the **Asymmetric Collaborative Evolution** (e.g., phase thresholds $T_s$, $T_e$) can be adjusted here [280].

## Project Structure

```text
DMGR/
├── Gen.py                      # Main generation script
├── confs/                      # Configuration files
│   └── pcb_gen.yml             # Main config
├── guided_diffusion/           # Core implementation
│   ├── ddim.py                 # DMGR sampler implementation (Gradient Rectification)
│   ├── script_util.py          # Utility functions
│   ├── gaussian_diffusion.py   # Base diffusion model
│   └── unet.py                 # U-Net architecture
├── utils/                      # Utility modules
│   ├── config.py               # Configuration management
│   ├── logger.py               # Logging utilities
│   └── drawer.py               # Visualization tools
├── data/                       # Dataset and references
│   ├── pcb.json                # PCB dataset configuration
│   └── Fig1.pdf                # Framework diagram
├── checkpoint/                 # Model checkpoints
│   ├── global-256.pt           # Global context model
│   └── defect-patch-64.pt      # Local defect model
└── images/                     # Generated outputs
    └── fj_ddim/                # DMGR results
```

## Citation and License

### Citation

If you find this code useful for your research, please cite our paper published in **IEEE Access**:

```bibtex
@article{luo2024dmgr,
  title={Dual-Manifold Gradient Rectification: Reconciling Topology and Texture in Industrial Anomaly Synthesis},
  author={Luo, Weihang and Huang, Jianxiongwen and Zhang, Zhijie and Zhang, Hongyi and Jiang, Huali and Gao, Xingen},
  journal={IEEE Access},
  volume={12},
  year={2024},
  doi={10.1109/ACCESS.2024.0429000}
}
```

This project is licensed under the [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) license. The code is released for academic research use only. For commercial use, please contact the authors.

**References in README:**
[1] W. Luo et al., "Dual-Manifold Gradient Rectification: Reconciling Topology and Texture in Industrial Anomaly Synthesis," IEEE Access, 2024.

```
