Dual-Manifold Gradient Rectification (DMGR)OverviewThis repository contains the official implementation of "Dual-Manifold Gradient Rectification: Reconciling Topology and Texture in Industrial Anomaly Synthesis", published in IEEE Access.Figure 1: The overall architecture of the Dual-Manifold Gradient Rectification (DMGR) framework.Key ContributionsThe reliability of automated industrial defect detection is often constrained by the scarcity of anomalous samples and the topological-textural conflict between defects and background. To address this, DMGR introduces:Dual-Manifold Gradient Rectification (DMGR): Unlike prior approaches that rely on heuristic blending or monolithic inpainting, DMGR reformulates defect synthesis as a deterministic trajectory rectification process. It explicitly models the interaction between a Global Background Manifold (Base Structural Field) and a Local Defect Manifold (Rectification Field).Physics-Grounded Spectral-Spatial Alignment: We introduce a Dynamic Multi-Scale Loss and an Uncertainty-Adaptive Spatial Gating mechanism. These ensure that high-frequency defect details are injected into the global trajectory without violating the spectral and spatial consistency of the background.Asymmetric Collaborative Evolution: A dynamic gradient scheduling strategy that coordinates Structural Anchoring (in early diffusion stages) and Textural Resonance (in later stages) to effectively harmonize global topology with local defect fidelity.Experimental results on a PCB defect dataset demonstrate that DMGR achieves superior semantic coherence and yields a 10.3% relative improvement in the downstream detector's mean Average Precision (mAP).InstallationPython 3.8+ recommendedPyTorch (CUDA recommended).Dependencies: numpy, pyyaml, pillow, matplotlibModel CheckpointsPre-trained ModelsPlease download the following pre-trained models and place them in the checkpoint/ directory. These models correspond to the dual manifolds described in the paper.1. Global Manifold Model (Base Structural Field)This model (Global U-Net) establishes the defect-free structural topology.Filename: global-256.ptDownload Link: Download from Google Drivewget -O checkpoint/global-256.pt "[https://drive.google.com/uc?export=download&id=1axJMm0fpg0v2HIApxz0IIaY0WTDKalCH](https://drive.google.com/uc?export=download&id=1axJMm0fpg0v2HIApxz0IIaY0WTDKalCH)"
2. Local Defect Model (Rectification Field Source)This model (Local U-Net) provides the expert reference for defect morphology.Filename: defect-patch-64.ptDownload Link: Download from Google Drivewget -O checkpoint/defect-patch-64.pt "[https://drive.google.com/uc?export=download&id=1GHT-q1XjF_aCmInp_g5gMruX3yih-iyM](https://drive.google.com/uc?export=download&id=1GHT-q1XjF_aCmInp_g5gMruX3yih-iyM)"
Directory Structure After Setupcheckpoint/
├── global-256.pt          # Global Background Manifold model
└── defect-patch-64.pt     # Local Defect Manifold model
Quick StartVerify Checkpoints: Ensure the model files are located in the checkpoint/ folder.Configuration: Use the provided config file confs/pcb_gen.yml.Run Synthesis:python Gen.py --conf_path confs/pcb_gen.yml
Outputs will be saved under the images/dmgr/ directory:images/dmgr/samples/: Final synthesized defect samples.images/dmgr/grid/: Visualization grids showing the rectification process steps.images/dmgr/crop/: Extracted defect patch crops used for rectification.Project StructureDMGR/
├── Gen.py                     # Main generation script (implements Trajectory Rectification Loop)
├── confs/                     # Configuration files
│   └── pcb_gen.yml            # Main synthesis configuration
├── guided_diffusion/          # Core implementation
│   ├── ddim.py                # DMGR Sampler with Gradient Rectification logic
│   ├── script_util.py         # Utility functions
│   ├── gaussian_diffusion.py  # Base diffusion model wrapper
│   └── unet.py                # U-Net architecture for Global/Local models
├── utils/                     # Utility modules
│   ├── loss.py                # Dynamic Multi-Scale Loss (Spectral Alignment)
│   ├── gating.py              # Uncertainty-Adaptive Spatial Gating
│   ├── logger.py              # Logging utilities
│   └── drawer.py              # Visualization tools
├── data/                      # Dataset and references
│   ├── pcb.json               # PCB dataset configuration
├── checkpoint/                # Model checkpoints
│   ├── global-256.pt          # Global model
│   └── defect-patch-64.pt     # Local model
└── images/                    # Output directory
CitationIf you find this code useful for your research, please cite our IEEE Access paper:@article{luo2024dmgr,
  title={Dual-Manifold Gradient Rectification: Reconciling Topology and Texture in Industrial Anomaly Synthesis},
  author={Luo, Weihang and Huang, Jianxiongwen and Zhang, Zhijie and Zhang, Hongyi and Jiang, Huali and Gao, Xingen},
  journal={IEEE Access},
  year={2024},
  publisher={IEEE},
  doi={10.1109/ACCESS.2024.0429000}
}
This project is licensed under the CC BY-NC-SA 4.0 license.
