# Predicting Routing Congestion from Chip Placements

APS360 (Applied Fundamentals of Deep Learning), University of Toronto, Fall 2026
Faria Samanta Akbar

## Goal
Predict where a chip layout will be **congested** (too many wires through one region) right after placement, before the slow routing step. The model takes three image-like maps of a placed layout and outputs horizontal and vertical routing-overflow heatmaps.

- **Inputs** (3 × 256 × 256): `macro_region`, `RUDY`, `RUDY_pin`
- **Outputs** (2 × 256 × 256): global-routing horizontal and vertical overflow
- **Model:** lightweight U-Net-style CNN encoder–decoder (PyTorch)
- **Baseline:** per-pixel linear regression on the same inputs ("calibrated RUDY")
- **Metrics:** NRMSE, SSIM, hotspot ROC-AUC, all on **held-out designs**

## Data
[CircuitNet-N28](https://circuitnet.github.io/): 10,242 layouts of six RISC-V designs in a 28 nm process.

| Split | Designs | Layouts |
|---|---|---|
| Train | RISCY-a, RISCY-b, RISCY-FPU-a | 5,830 |
| Validation | RISCY-FPU-b | 1,248 |
| Test (unseen core) | zero-riscy-a, zero-riscy-b | 3,164 |

The split is by design, not random, so test scores measure generalization to chips the model has never seen.

## Repository
| File | Purpose |
|---|---|
| `circuitnet_data_check.ipynb` | Downloads the needed CircuitNet files in Colab, verifies them, builds a preprocessed subset ([open in Colab](https://colab.research.google.com/drive/1TjeERbnvFhNeIo_u3M3cmsqiBg2814pv?usp=sharing)) |

More code (preprocessing, baseline, model, training) will be added as the project progresses.

## Status
- [x] Proposal
- [x] Data downloaded and integrity-checked
- [ ] Preprocessing pipeline
- [ ] Baseline
- [ ] U-Net training and evaluation

## References
- Chai et al., *CircuitNet: An Open-Source Dataset for Machine Learning Applications in EDA*, Sci. China Inf. Sci., 2022.
- Liu et al., *Global Placement with Deep Learning-Enabled Explicit Routability Optimization*, DATE 2021.
- Spindler & Johannes, *Fast and Accurate Routing Demand Estimation for Efficient Routability-Driven Placement*, DATE 2007.
