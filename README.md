 # 🧠 Pattern-Recognition

> A **deep-learning pattern recognition** project that classifies 3D-mesh-derived patches into **edge / texture / non-texture** categories using multiple geometric representations (depth, surface-normal azimuth, surface-normal elevation).

[![Python](https://img.shields.io/badge/python-3-blue)]()
[![PyTorch](https://img.shields.io/badge/framework-PyTorch-EE4C2C)]()
[![Notebook](https://img.shields.io/badge/code-Jupyter-orange)]()
[![Colab](https://img.shields.io/badge/runs%20on-Google%20Colab-yellow)]()

---

## 📌 Overview

A research-style coursework project where 3D mesh models are sliced into 2D **patches** under three different geometric representations, and a CNN is trained to classify each patch as **edge**, **texture**, or **non-texture**.

Two patch resolutions are studied — **14×14** and **32×32** — and four data variants are evaluated:

| Representation | What it encodes |
|---|---|
| **Local depth** | Per-pixel depth around the patch center |
| **Normal azimuth** | Azimuth angle of the surface normal |
| **Normal elevation** | Elevation angle of the surface normal |
| **All (merged)** | All three representations stacked together |

For each `(resolution, representation)` combo, a separate model is trained, and the best validation checkpoint is saved for testing.

Code:	the codes  for the training and testing. The patern_recognition.ipynb contains all the code
	and is generated using Google Colab. It can also be opened in jypiter notebook. Python 3.

dataset: contains the patches used for the training. The folders are divided in IMG14 and IMG32 and
	 inside of each are the different representations (local depth, normal azimuth and normal elevation)
	and all of them merged together in the "all" folder. Each of them is divided in 3 folders :train, test, val
	and these ones are also grouped in 3 subfolders : edge, non_texture and texture. 
	That depends on the label of the patch. 

Doc: The papers readed for this project and some useful links.

mesh grid generation: This folder contains mesh models, the related descriptors and the code to generate the patches

models: contains the trained models which have the best accuracy on validation. Used for the testing.
	_model_azimuth_32_13.pt : azimuth : the representation
				  32 : the dimension of the patch
				  13 : the number of the epoch 

train_test_results: contains the results of the testing. Each folder has the results depending on 
			the dimension of the patch and the representation. 
			Each file consists of 2 parts:
			  - The first are the results of the training and validation of each epoch.
			   In the end there is the best accuracy of the validation and the model is saved for the testing.
			  - The second are the results of the testing. In the end is the average testing result

## 🗂️ Project Structure

```
Pattern-Recognition/
├── Code/
│   └── pattern_recognition.ipynb   # Full training + testing notebook (Colab/Jupyter)
│
├── dataset/
│   ├── IMG14/                      # 14×14 patches
│   │   ├── local_depth/
│   │   ├── normal_azimuth/
│   │   ├── normal_elevation/
│   │   └── all/                    # merged representations
│   │       ├── train/{edge, non_texture, texture}
│   │       ├── test/{edge, non_texture, texture}
│   │       └── val/{edge, non_texture, texture}
│   └── IMG32/                      # 32×32 patches (same layout)
│
├── Doc/                            # Background papers + useful links
│
├── mesh grid generation/           # Mesh models, descriptors, patch-extraction code
│
├── models/                         # Saved best-validation checkpoints (.pt)
│   └── _model_azimuth_32_13.pt     # Naming: <repr>_<patch_size>_<best_epoch>
│
└── train_test_results/             # Per-experiment training logs and test summaries
```

### Model checkpoint naming convention

`_model_<representation>_<patch_size>_<epoch>.pt`

Example — `_model_azimuth_32_13.pt`:
- **azimuth** — representation
- **32** — patch dimension (32×32)
- **13** — epoch with best validation accuracy

### Results-file convention

Each file in `train_test_results/` is split into two sections:

1. **Training & validation log** — per-epoch loss/accuracy with the best-epoch summary at the end (the model from this epoch is saved for testing)
2. **Testing log** — per-batch test results with average accuracy reported at the end

## 🚀 Setup & Run

### Option A — Google Colab (recommended)

The notebook (`Code/pattern_recognition.ipynb`) is built to run on Google Colab with GPU acceleration. Open it, upload the `dataset/` and `models/` folders to your Drive, and `Runtime → Run all`.

### Option B — Local Jupyter

```bash
# Create a virtual env
python3 -m venv venv
source venv/bin/activate

# Install
pip install jupyter torch torchvision numpy matplotlib pillow

# Launch
jupyter notebook Code/pattern_recognition.ipynb
```

## 🧪 Workflow

```
┌───────────────────────┐
│  Mesh models (.obj)   │
└──────────┬────────────┘
           │  patch extraction (mesh grid generation/)
           ▼
┌─────────────────────────────────────┐
│  dataset/IMG{14,32}/<rep>/          │
│        train / val / test           │
│           edge / texture / non_text │
└──────────┬──────────────────────────┘
           │
           ▼
┌─────────────────────────────────────┐
│  pattern_recognition.ipynb          │
│  • CNN trained per (rep, size)      │
│  • best-val epoch saved → models/   │
│  • test eval on held-out set        │
└──────────┬──────────────────────────┘
           │
           ▼
┌─────────────────────────────────────┐
│  train_test_results/                │
│  per-experiment train/val/test logs │
└─────────────────────────────────────┘
```

## 📚 Documentation

The `Doc/` folder collects the **research papers** referenced during the project and **useful links** for surface-normal estimation, depth-map descriptors, and CNN architectures used as a baseline.

## 🔬 Companion Project

➡️ For a related image-quality study, see [CMOS-VS-CCD](https://github.com/denisvreshtazi/CMOS-VS-CCD).

## 💡 Possible Extensions

- Replace the baseline CNN with a **ResNet** or **EfficientNet** backbone
- Use **early fusion** vs **late fusion** of the three representations and compare
- Add **data augmentation** (rotation, jitter on normals)
- Convert from notebook → modular package with `train.py`, `eval.py`, `model.py`

## 👤 Author

**Denis Vreshtazi** — [GitHub](https://github.com/denisvreshtazi)

