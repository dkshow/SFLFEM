# SFLFEM

**SFLFEM: A Frequency-Enhanced Mamba Framework for Selectivity Personalized Federated Breast Ultrasound Diagnosis**

## Overview

SFLFEM is a frequency-enhanced Mamba framework designed for personalized federated breast ultrasound diagnosis. It integrates frequency-domain feature enhancement with Mamba-based visual representation learning, aiming to improve breast ultrasound classification under multi-client and non-IID data distributions.

## Repository Structure

```text
├── model/              # Model implementations of SFLFEM and related modules
├── federated/          # Federated learning and personalized aggregation strategies
├── preprocess/         # Data preprocessing for breast ultrasound images
├── configs/            # Configuration files for experimental settings
├── train.py            # Training script
├── evaluate.py         # Evaluation and metrics
├── utils/              # Utility functions
└── README.md
```

## Requirements

* Python 3.8
* PyTorch
* CUDA
* NumPy
* scikit-learn
* OpenCV
* einops

## Datasets

Due to privacy and license restrictions, the breast ultrasound datasets used in this study are not publicly released in this repository.

Please organize the datasets in the `data/` directory as follows:

```text
data/
├── client_1/
├── client_2/
├── client_3/
└── test/
```

Each client folder should contain breast ultrasound images and the corresponding label file.

## Usage

```bash
# Training
python train.py --config configs/sflfem.yaml

# Evaluation
python evaluate.py --config configs/sflfem.yaml --checkpoint best_model.pth
```



## Contact
For questions, please contact Xu He (hxwho123321@gmail.com).
