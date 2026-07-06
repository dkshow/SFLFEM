# SFLFEM

Official code repository for **“SFLFEM: A Frequency-Enhanced Mamba Framework for Selectivity Personalized Federated Breast Ultrasound Diagnosis.”**

> **Status:** Code, configuration files, and reproduction instructions are being organized and will be released progressively.

## Overview

Breast ultrasound diagnosis is challenging because ultrasound images are often affected by speckle noise, domain shifts across medical centers/devices, and heterogeneous data distributions. Centralized training may also be limited by privacy concerns in clinical scenarios.

**SFLFEM** is a frequency-enhanced Mamba-based personalized federated learning framework for breast ultrasound diagnosis. The framework aims to improve diagnostic performance under non-IID client distributions by combining:

* **Frequency-enhanced feature modeling** for ultrasound-specific texture and structural information.
* **Mamba-based long-range dependency modeling** for efficient medical image representation learning.
* **Selective personalized federated learning** to better adapt global knowledge to client-specific distributions.
* **Privacy-preserving multi-client training** without centralizing raw ultrasound images.

## Framework

<p align="center">
  <img src="figures/framework.png" width="800">
</p>

The overall pipeline contains three major components:

1. **Local breast ultrasound feature extraction**
   Each client trains on its own local ultrasound data without sharing raw images.

2. **Frequency-enhanced Mamba representation learning**
   Frequency-aware modules are used to enhance discriminative ultrasound patterns, while Mamba blocks model long-range dependencies efficiently.

3. **Selective personalized federated optimization**
   The server aggregates useful shared knowledge, while personalized components are adapted to client-specific data distributions.

## News

* `[TODO]` Initial README framework released.
* `[TODO]` Code will be released after paper acceptance / revision completion.
* `[TODO]` Pretrained checkpoints and training logs will be provided when available.

## Repository Structure

```text
SFLFEM/
├── configs/                 # YAML configuration files
├── datasets/                # Dataset preparation instructions
├── sflfem/
│   ├── models/              # Frequency-enhanced Mamba model
│   ├── federated/           # Federated training and aggregation modules
│   ├── datasets/            # Dataset loader and preprocessing
│   ├── trainers/            # Training and evaluation pipeline
│   └── utils/               # Metrics, logging, seed control, etc.
├── scripts/                 # Example running scripts
├── checkpoints/             # Pretrained models or saved checkpoints
├── figures/                 # Framework and result figures
├── requirements.txt
└── README.md
```

## Installation

### 1. Clone this repository

```bash
git clone https://github.com/[YOUR_USERNAME]/SFLFEM.git
cd SFLFEM
```

### 2. Create environment

```bash
conda create -n sflfem python=3.8 -y
conda activate sflfem
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

A recommended environment is:

```text
Python >= 3.8
PyTorch >= [TODO]
CUDA >= [TODO]
timm
einops
scikit-learn
numpy
pandas
opencv-python
matplotlib
```

> Note: Mamba-related dependencies may depend on the CUDA/PyTorch version. Please check your local environment before installation.

## Dataset Preparation

Due to privacy and license restrictions, clinical breast ultrasound datasets used in this study may not be directly redistributed through this repository.

Please organize your dataset as follows:

```text
data/
├── client_1/
│   ├── images/
│   ├── labels.csv
│   └── masks/              # optional
├── client_2/
│   ├── images/
│   ├── labels.csv
│   └── masks/
├── client_3/
│   ├── images/
│   ├── labels.csv
│   └── masks/
└── test/
    ├── images/
    ├── labels.csv
    └── masks/
```

The label file should follow this format:

```csv
image_name,label
case_0001.png,0
case_0002.png,1
```

where:

```text
0 = benign / negative
1 = malignant / positive
```

Please update dataset paths in:

```text
configs/sflfem_bus.yaml
```

Example:

```yaml
data_root: ./data
clients:
  - name: client_1
    image_dir: ./data/client_1/images
    label_file: ./data/client_1/labels.csv
  - name: client_2
    image_dir: ./data/client_2/images
    label_file: ./data/client_2/labels.csv
test:
  image_dir: ./data/test/images
  label_file: ./data/test/labels.csv
```

## Quick Start

### Federated training

```bash
bash scripts/train_federated.sh
```

or

```bash
python train.py \
  --config configs/sflfem_bus.yaml \
  --mode train \
  --num_clients 4 \
  --rounds 100 \
  --local_epochs 5 \
  --batch_size 16
```

### Global model evaluation

```bash
bash scripts/test_global.sh
```

or

```bash
python test.py \
  --config configs/sflfem_bus.yaml \
  --checkpoint checkpoints/global_model.pth \
  --mode global
```

### Personalized model evaluation

```bash
bash scripts/test_personalized.sh
```

or

```bash
python test.py \
  --config configs/sflfem_bus.yaml \
  --checkpoint checkpoints/personalized_client_1.pth \
  --mode personalized \
  --client_id 1
```

## Main Configuration

Key parameters can be modified in `configs/sflfem_bus.yaml`:

```yaml
seed: 42
num_clients: 4
communication_rounds: 100
local_epochs: 5
batch_size: 16
learning_rate: 0.0001

model:
  name: SFLFEM
  backbone: FrequencyEnhancedMamba
  num_classes: 2

federated:
  algorithm: selective_personalized_fl
  aggregation: selective
  personalization: true

training:
  optimizer: AdamW
  scheduler: cosine
  loss: cross_entropy
```

## Results

The detailed results will be updated after paper acceptance.

| Method                   | ACC        | AUC        | SEN        | SPE        | F1         |
| ------------------------ | ---------- | ---------- | ---------- | ---------- | ---------- |
| FedAvg                   | [TODO]     | [TODO]     | [TODO]     | [TODO]     | [TODO]     |
| FedProx                  | [TODO]     | [TODO]     | [TODO]     | [TODO]     | [TODO]     |
| Personalized FL baseline | [TODO]     | [TODO]     | [TODO]     | [TODO]     | [TODO]     |
| **SFLFEM**               | **[TODO]** | **[TODO]** | **[TODO]** | **[TODO]** | **[TODO]** |

## Pretrained Models

Pretrained weights will be provided when available.

| Model               | Dataset Setting            | Link   |
| ------------------- | -------------------------- | ------ |
| SFLFEM-global       | Multi-client BUS diagnosis | [TODO] |
| SFLFEM-personalized | Client-specific diagnosis  | [TODO] |

## Reproducibility Checklist

* [ ] Source code
* [ ] Environment file
* [ ] Dataset preparation instructions
* [ ] Training scripts
* [ ] Evaluation scripts
* [ ] Configuration files
* [ ] Pretrained checkpoints
* [ ] Main experimental results
* [ ] Citation information

## Citation

If you find this repository useful, please consider citing our paper:

```bibtex
@article{TODO_sflfem,
  title   = {SFLFEM: A Frequency-Enhanced Mamba Framework for Selectivity Personalized Federated Breast Ultrasound Diagnosis},
  author  = {[TODO]},
  journal = {[TODO]},
  year    = {[TODO]}
}
```

## Acknowledgements

This repository may build upon or refer to open-source implementations of PyTorch, Mamba/State Space Models, and federated learning frameworks. We sincerely thank the authors and contributors of these projects.

## License

This project is released under the `[TODO: MIT / Apache-2.0 / CC BY-NC 4.0 / custom academic license]` license.

## Contact

For questions or collaboration, please contact:

```text
[YOUR NAME]
[YOUR EMAIL]
[YOUR INSTITUTION]
```
