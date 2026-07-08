# Tutorial: Multiple Myeloma Datasets

A hands-on tutorial on applying AI to Multiple Myeloma diagnosis from bone marrow smear images, built around two public plasma cell datasets from LabIA-UFBA.

## Datasets

| # | Dataset | Paper | Original Model |
|---|---------|-------|-----------------|
| 1 | [Multiple Myeloma Dataset](https://github.com/LabIA-UFBA/Multiple-Myeloma-Dataset) | Andrade et al. (2024), *Scientific Reports* 14:11176 | YOLOv7 |
| 2 | [PCMMD](https://github.com/LabIA-UFBA/MMDB) | Andrade et al. (2025), *Scientific Data* 12:161 | YOLOv8 |

- **Dataset 1** — 1,024 bone marrow aspirate smear images, Wright-Giemsa staining, smartphone-captured, single-class YOLO bounding box annotations, 10-fold validation.
- **Dataset 2 (PCMMD)** — 10 patients, detection + segmentation annotations, CC-BY-4.0, 5-fold validation.

This tutorial reproduces the original pipelines using **YOLO26** (latest Ultralytics release) instead of the original YOLOv7/YOLOv8, favoring fast, live-demoable runs (nano model, few epochs) over state-of-the-art accuracy.

## Notebooks

1. **`01_image_presentation.ipynb`** — Downloads both datasets and visualizes images with their YOLO annotations.
2. **`02_training_yolo.ipynb`** — Fine-tunes YOLO26n on Dataset 1 (single class), shows training curves, and evaluates on the test set.
3. **`03_diagnosis.ipynb`** — Trains a 2-class (plasma / non-plasma) detector on PCMMD, aggregates per-patient detections into a plasma cell percentage, and applies a clinical threshold (>10%) for diagnosis.
4. **`04_synthetic_data_augmentation.ipynb`** — Builds a synthetic data pipeline: per-slide statistics (KDE) → cell crops/masks → color deconvolution (Beer-Lambert) → DDPM (diffusion) training → synthetic slide composition → baseline vs. augmented comparison.

Run them in order; each notebook downloads any data it needs if not already present.

## Setup

```bash
pip install -r requirements.txt
```

Requires Python with Jupyter (`ipykernel`), PyTorch, Ultralytics YOLO, and Hugging Face `diffusers` for the generative pipeline in notebook 04.

## Data & Models

Datasets and model weights are downloaded automatically by the notebooks into `data/` and are not tracked in git (see `.gitignore`). No manual setup is required beyond internet access on first run.

## Citation

If you use these datasets, please cite the original papers:

- Andrade et al. (2024). *Scientific Reports*, 14:11176.
- Andrade et al. (2025). *Scientific Data*, 12:161.
