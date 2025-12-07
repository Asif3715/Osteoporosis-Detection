# Multimodal Fusion of Deep Spatial Features and Clinical Metadata for Enhanced Osteoporosis Classification in Knee X-rays

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/Framework-PyTorch-red)](https://pytorch.org/)
[![Status](https://img.shields.io/badge/Status-Completed-success)]()

## 📌 Project Overview
This repository contains the official implementation of the research paper **"Multimodal Fusion of Deep Spatial Features and Clinical Metadata for Enhanced Osteoporosis Classification"**.

Osteoporosis is often diagnosed too late using expensive DEXA scans. This project aims to democratize early detection by classifying **Knee X-rays** into Normal, Osteopenia, and Osteoporosis using standard X-ray imaging fused with clinical patient history.

We propose a **Late Fusion Architecture** that integrates:
1.  **Visual Features:** Extracted using a Domain-Adapted **ResNet50** (pre-trained on 2,800+ knee X-rays).
2.  **Clinical Metadata:** Patient history (Age, BMI, Gender, Fracture History) processed via an ANN.
3.  **Self-Supervised Learning (SSL):** Exploration of Masked Autoencoders (ViT-MAE) to learn features without labels.

---

## 🚀 Key Results
Our proposed **ResNet50 Fusion** model outperforms unimodal baselines and naive fusion approaches, particularly in detecting **Osteopenia** (the critical early stage).

| Model | Modality | Accuracy | Osteopenia Recall |
| :--- | :---: | :---: | :---: |
| **EfficientNet-B3** | Image Only | 66.0% | 0.61 |
| **VGG19** | Image Only | 86.0% | 0.86 |
| **SSL ViT (MAE)** | Image Only | 80.5% | 0.76 |
| **VGG19 Fusion** | Image + Tabular | 75.0% | 0.50 |
| **Proposed ResNet50 Fusion** | **Image + Tabular** | **87.5%** | **0.97** |

> **Key Finding:** While VGG19 was a strong feature extractor, its high-dimensional feature vector overwhelmed the tabular data during fusion. ResNet50's compact representation allowed for successful multimodal integration.

---

## 📂 Dataset Strategy
We utilized a **Dual-Dataset Strategy** to overcome the scarcity of labeled medical data:

1.  **Source Dataset (Big):** Aggregated 2,839 images from Kaggle, OAI, and Mendeley V1. Used for **Domain Adaptation** and **SSL Pre-training**.
2.  **Target Dataset (Small):** [Mendeley Data V2](https://data.mendeley.com/datasets/fxjm8fb6mw/2). Contains ~240 images linked with granular clinical metadata (Age, Gender, BMI, etc.). Used for **Fusion Training**.

---

## 🧠 Methodology & Notebooks
The project is divided into the following experimental notebooks:

### 1. Data Preparation
* `1_Data_Preprocessing.ipynb`: Cleaning clinical Excel sheets, imputing missing values, and binary encoding categorical features.

### 2. Baseline Experiments
* `2_Baseline_EfficientNet.ipynb`: Implementation of EfficientNet-B3 (Failed Baseline).
* `3_Baseline_VGG19.ipynb`: Implementation of VGG19 with Transfer Learning (Strong Baseline).

### 3. Self-Supervised Learning (SSL)
* `ssl-knee-mae-training.ipynb`: Pre-training a **Masked Autoencoder (MAE)** on unlabeled X-rays.
* `osteo-classification-using-ssl-encoder.ipynb`: Fine-tuning the SSL encoder (ViT) for classification.

### 4. Proposed Fusion Architecture
* `6_Proposed_ResNet50_Adaptation.ipynb`: Domain adaptation of ResNet50 on the large Source Dataset.
* `7_Final_Fusion_Model.ipynb`: **The Best Model.** Loading pre-trained ResNet weights, freezing them, and fusing with tabular data.

---

## 🛠️ Installation & Usage

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
   cd YOUR_REPO_NAME
   
