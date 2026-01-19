# 🥭 Indian Mango Variety Classifier (Transfer Learning)

This project implements an end-to-end **image classification system** to identify **Indian mango varieties** using **deep learning and transfer learning**.

The model classifies mango images into one of six varieties, **independent of ripeness** (ripe and unripe images are mixed).

---

## 📌 Project Objective

- **Input:** Image of a single mango (ripe or unripe)
- **Output:** Mango variety (class label)

> ⚠️ This project focuses only on **variety classification**.  
> Ripeness classification is planned as future work.

---

## 🗂️ Dataset Overview

- **Total images:** 2633
- **Number of classes:** 6
- **Image type:** Real-world images with varying lighting, angles, and backgrounds

### Class Distribution

| Mango Variety | Images |
|--------------|--------|
| AMRAPALLI | 460 |
| ARKA_NEELACHAL_KESARI | 541 |
| BANGANPALLI | 443 |
| DASHEHARI | 438 |
| SUVARNA_REKHA | 292 |
| TOTAPURI | 464 |

- Dataset is **slightly imbalanced**
- Both ripe and unripe images are included in each class

---

## 🧠 Methodology

### 🔹 Model
- **EfficientNet-B0**
- Pretrained on **ImageNet**
- Transfer learning approach

### 🔹 Training Strategy
1. **Feature Extraction**
   - Backbone frozen
   - Only classifier head trained
2. **Fine-Tuning**
   - Top layers of EfficientNet unfrozen
   - Small learning rate for stable improvement

### 🔹 Data Augmentation (Training Only)
- Random horizontal flip
- Random rotation
- Color jitter

### 🔹 Class Imbalance Handling
- Class-weighted CrossEntropy loss
- Improved performance for minority classes

---

## 📊 Dataset Split

| Split | Images |
|------|--------|
| Training | ~2106 |
| Validation | ~263 |
| Test | ~264 |

- Test set is **never used during training**
- Final evaluation is performed only on the test set

---

## 📈 Results

### ✅ Final Test Accuracy
**90.9%**

### 📊 Classification Report (Test Set)

| Class | Precision | Recall | F1-score |
|-----|-----------|--------|---------|
| AMRAPALLI | 0.9348 | 0.9556 | 0.9451 |
| ARKA_NEELACHAL_KESARI | 0.9672 | 1.0000 | 0.9833 |
| BANGANPALLI | 0.7500 | 0.8333 | 0.7895 |
| DASHEHARI | 0.9767 | 0.7500 | 0.8485 |
| SUVARNA_REKHA | 0.7647 | 1.0000 | 0.8667 |
| TOTAPURI | 1.0000 | 0.9524 | 0.9756 |

- Strong generalization on unseen data
- Most confusions occur between visually similar varieties

---

## 🧩 Confusion Matrix (Test Set)

- Errors mainly occur between:
  - **BANGANPALLI ↔ DASHEHARI**
  - **BANGANPALLI ↔ SUVARNA_REKHA**

These are expected due to fine-grained visual similarity.

