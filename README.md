# YOLOv11s vs Faster R-CNN for Object Detection in Adverse Weather

## Overview

This repository contains the implementation and results of my MSc dissertation:

**Performance Analysis of Object Detection Models in Adverse Weather for Autonomous Vehicles**

The project compares **YOLOv11s** and **Faster R-CNN** for road-object detection under **fog, rain, and snow**. The comparison focuses on three aspects:

1. Detection accuracy
2. Inference speed
3. Generalisation to unseen datasets

The experiments were conducted using the **DAWN**, **ACDC**, and **BDD100K** datasets.

## Research Objectives

The main objectives were to:

* Compare the detection accuracy of YOLOv11s and Faster R-CNN.
* Evaluate the trade-off between accuracy and inference speed.
* Analyse model performance under fog, rain, and snow.
* Assess cross-dataset generalisation between DAWN and ACDC.
* Perform external validation using unseen BDD100K images.
* Improve reliability by repeating experiments with three random seeds: **42, 123, and 456**.

## Datasets

### DAWN

DAWN contains real-world road images captured under adverse weather conditions. The experiments used images representing:

* Fog
* Rain
* Snow

DAWN must be downloaded manually before running the related notebooks.

### ACDC

ACDC is an autonomous-driving dataset containing images captured under adverse conditions. The project uses its fog, rain, and snow subsets.

### BDD100K

BDD100K was used as an unseen external dataset to evaluate how well the trained models generalise beyond their original training datasets.

### Object Classes

The datasets were harmonised into six common classes:

* Person
* Bicycle
* Car
* Motorcycle
* Bus
* Truck

## Models

### YOLOv11s

YOLOv11s was implemented using the **Ultralytics** framework and initialised with COCO-pretrained weights.

Main configuration:

* Image size: 640 × 640
* Batch size: 16
* Maximum epochs: 100
* Early-stopping patience: 10
* Random seeds: 42, 123, and 456

### Faster R-CNN

Faster R-CNN with a **ResNet-50 Feature Pyramid Network** backbone was used.

The implementations were based on Detectron2 R50-FPN 3x for the ACDC experiments

Main configuration:

* Learning rate: 0.001
* Batch size: 4
* COCO-pretrained weights
* Random seeds: 42, 123, and 456

## Experimental Design

The evaluation was divided into three phases:

### Phase 1: In-Domain Evaluation

Each model was trained and tested on the same dataset:

* DAWN → DAWN
* ACDC → ACDC

### Phase 2: Cross-Dataset Evaluation

The trained models were evaluated on a different dataset:

* DAWN → ACDC
* ACDC → DAWN

### Phase 3: External Validation

Models trained on DAWN or ACDC were evaluated on unseen BDD100K images.

## Evaluation Metrics

The models were compared using:

* mAP50-95
* mAP50
* mAP75
* Precision
* Recall
* F1-score
* Inference speed in frames per second
* Weather-specific detection performance

## Key Results

| Dataset | Model        | mAP50-95 |  FPS |
| ------- | ------------ | -------: | ---: |
| DAWN    | YOLOv11s     |   0.3396 | 80.3 |
| DAWN    | Faster R-CNN |   0.4321 | 20.3 |
| ACDC    | YOLOv11s     |   0.3329 | 84.2 |
| ACDC    | Faster R-CNN |   0.4128 | 16.1 |

The main findings were:

* Faster R-CNN achieved higher detection accuracy on both datasets.
* YOLOv11s provided substantially faster inference.
* Rain was generally the most challenging weather condition.
* Both models experienced a significant performance decrease during cross-dataset evaluation.
* Models trained on the more diverse ACDC dataset showed better external generalisation to BDD100K.

These results demonstrate the trade-off between the higher accuracy of Faster R-CNN and the real-time performance of YOLOv11s.

## Repository Structure

```text
.
├── Notebooks/
│   ├── 00_environment_setup.ipynb
│   ├── dataset_preparation/
│   ├── YOLOv11s/
│   ├── Faster_RCNN/
│   └── results_analysis/
├── Results/
│   ├── figures/
│   └── tables/
└── README.md
```

The repository contains selected notebooks and results from the complete dissertation project.

Datasets, trained model weights, and other large files are not included because of their size and distribution conditions.

## Requirements

The project was developed and executed using **Google Colab**.

Main libraries:

* Python 3
* PyTorch
* Ultralytics
* Detectron2
* NumPy 1.26.4
* Pandas
* OpenCV
* Matplotlib
* Seaborn
* Scikit-learn
* pycocotools

The required installation commands are already included in the notebooks.

## Hardware

The official training and evaluation experiments were conducted using a paid Google Colab environment with an **NVIDIA A100 GPU**.

The notebooks may also run on other CUDA-compatible GPUs, but training duration and inference-speed results may differ.

## Running the Project

1. Open the required notebook in Google Colab.
2. Enable a GPU runtime.
3. Run the installation and environment-setup cells.
4. Connect Google Drive when requested.
5. Configure the dataset path in the notebook.
6. Run the data-preparation, training, or evaluation cells in order.

For the DAWN experiments, the dataset must first be downloaded manually and stored in the expected Google Drive directory.

The other dataset-preparation instructions are provided inside the relevant notebooks.

## Reproducibility

The experiments were repeated using three random seeds: 42, 123, 456


Deterministic settings were enabled where supported. Minor differences may still occur depending on the GPU, framework version, and execution environment.

## Author

**Koloina Mioty Soa Razakahariseheno**

MSc Artificial Intelligence with Machine Learning
University of Technology, Mauritius
