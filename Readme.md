# Multiclass Hepatic Tumor & Vessel Segmentation using Swin-UNet

## Project Overview

This project focuses on the **automated multiclass segmentation of hepatic (liver) tumors and blood vessels** from medical imaging data (CT/MRI). It leverages a **Transformer-based Swin-UNet architecture**, combining the strengths of Vision Transformers and U-Net–style encoders/decoders to achieve high-precision pixel-level segmentation.

The system is designed to assist **clinical diagnosis, surgical planning, and medical decision-making** by providing accurate delineation of tumors and vascular structures.

> **Role Clarification:** The model and system were **designed and developed by me**, while the project was formally **presented by another team member**.

---

##  Motivation

* Manual tumor and vessel segmentation is **time-consuming, subjective, and error-prone**
* Accurate delineation is critical for **hepatic cancer diagnosis and surgery planning**
* Conventional CNN-based models struggle with **long-range dependencies and complex vessel structures**

---

##  Architecture

The  model is based on **Swin-UNet**, a pure Transformer U-shaped architecture:

* **Swin Transformer Encoder**

  * Patch embedding with hierarchical feature extraction
  * Shifted Window Multi-Head Self-Attention (SW-MSA)
  * Captures both local and global contextual information

* **U-Net–Style Decoder**

  * Patch expanding layers for upsampling
  * Skip connections to preserve fine-grained spatial details

* **Loss Function**

  [ L = \alpha L_{Dice} + (1 - \alpha) L_{CE} ]

  * Dice Loss: Handles class imbalance
  * Cross-Entropy Loss: Improves class-wise discrimination

---

##  Dataset

* **Source:** Medical Segmentation Decathlon (MSD)
* **Total Images:** 2,154
* **Classes:**

  * Tumor
  * Vessel
  * Background

### Data Split

| Split      | Percentage | Images |
| ---------- | ---------- | ------ |
| Training   | 60%        | 1,584  |
| Validation | 20%        | 285    |
| Testing    | 20%        | 285    |

---

## Training Details

* Framework: **PyTorch**
* Optimizer: Adam (default settings)
* Loss: Dice + Cross-Entropy
* Early stopping based on validation loss

The model demonstrates **stable convergence**, with training and validation losses closely aligned, indicating minimal overfitting.

---

##  Results

### Quantitative Comparison

| Model                | Avg Dice (%) | Tumor Dice (%) | Vessel Dice (%) | HD95 (mm) ↓ |
| -------------------- | ------------ | -------------- | --------------- | ----------- |
| U-Net (Baseline)     | 76.85        | 82.10          | 71.60           | 39.72       |
| TransUNet            | 77.48        | 84.35          | 70.61           | 31.69       |
| **Swin-UNet (Ours)** | **81.24**    | **89.42**      | **83.06**       | **21.55**   |

### Class-wise Performance

| Class      | Dice | Precision | Recall |
| ---------- | ---- | --------- | ------ |
| Tumor      | 0.89 | 0.91      | 0.88   |
| Vessel     | 0.82 | 0.84      | 0.80   |
| Background | 0.98 | 0.99      | 0.98   |

---

##  Key Outcomes

* Significant improvement over baseline U-Net
* Better vessel continuity and tumor boundary delineation
* Effective modeling of spatial relationships using shifted-window attention

---

##  Tech Stack

* **Python**
* **PyTorch**
* **Swin Transformer**
* **Medical Image Processing**
* **Deep Learning for Healthcare**

---

