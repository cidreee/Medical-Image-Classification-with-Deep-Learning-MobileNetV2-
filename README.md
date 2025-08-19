# Medical-Image-Classification-with-Deep-Learning-MobileNetV2-
## Deep Learning-based Classification of Endoscopic Images

This repository contains the implementation of a deep learning pipeline for classifying gastrointestinal endoscopic images into three disease categories: **esophagitis**, **polyps**, and **ulcerative colitis**.  
The project is based on the research paper:  
*Deep Learning-based Classification of Endoscopic Images with MobileNetV2 and Preprocessing* by **Valeria Andrade (2025, Universidad Panamericana, Aguascalientes, México)**.

---

##  Abstract
This project demonstrates a deep learning approach for automated diagnosis of gastrointestinal diseases using **transfer learning** with **MobileNetV2** and domain-specific preprocessing.  
Key highlights:
- Dataset: 3,000 endoscopic images (from the **Kvasir dataset**).
- Preprocessing: removal of ScopeGuide artifacts, image normalization, and deduplication with perceptual hashing.
- Data Augmentation: extensive transformations (rotations, flips, brightness/contrast, blur, HSV shifts).
- Model: MobileNetV2 backbone + dense layer, dropout, and softmax classifier.
- Training Strategy: two-phase training (frozen base → fine-tuning).

---

## Dataset
- Source: [Kvasir dataset](https://datasets.simula.no/kvasir/)  
- Classes included:
  - Esophagitis
  - Polyps
  - Ulcerative colitis
- Split ratio: **70% training / 15% validation / 15% testing**
- Deduplication ensured via **perceptual hashing** to prevent data leakage.

---

## Methodology
### Preprocessing
- Removal of green ScopeGuide box (using HSV color filtering).
- Cropping of bright regions.
- Normalization to **224×224** resolution.

### Data Augmentation
- Random 90° rotations, flips, scaling, and shifts.
- Brightness/contrast adjustments.
- Gaussian blur, gamma correction, HSV shifts.

### Model
- **MobileNetV2** pretrained on ImageNet.
- Architecture:
  - Global Average Pooling
  - Dense layer (256 ReLU units + L2 regularization)
  - Dropout (0.3)
  - Softmax output (3 classes)

### Training
- Batch size: **32**
- Optimizer: **Adam**
- Loss: **Categorical cross-entropy**
- Callbacks: Early stopping, TensorBoard, WandB logging
- Two phases:
  1. Train classifier head (frozen backbone).
  2. Fine-tune all layers (low learning rate).

---

## Results
- **Accuracy:** 94.89%  
- **Precision (macro):** 94.39%  
- **Recall (macro):** 93.56%  
- **F1 Score (macro):** 93.47%  
- **Test Loss:** 0.2026  

### Per-class Performance:
| Class            | Precision | Recall | F1 Score | Specificity |
|------------------|-----------|--------|----------|-------------|
| Esophagitis      | 94.34%    | 100%   | 97.09%   | 97.00%      |
| Polyps           | 99.26%    | 90.00% | 94.41%   | 99.67%      |
| Ulcerative Colitis | 91.61%  | 94.67% | 93.11%   | 95.67%      |

---

## Author
- **Valeria Andrade**  
🎓 Universidad Panamericana – Campus Aguascalientes
