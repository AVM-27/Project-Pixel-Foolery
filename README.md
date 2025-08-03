# 🧠 Project Pixel Foolery: Fooling Neural Networks with Few-Pixel Attacks

This project explores the vulnerability of deep convolutional networks to pixel-level adversarial attacks. We apply **Differential Evolution (DE)** to perform **black-box perturbations** on trained **PureCNN** and **Modified ResNet** models on **CIFAR-10** and **binary class subsets (Cat vs Dog)**. The goal: reduce true class confidence and induce misclassification by tweaking just 1–5 pixels.

---

## 📁 Repository Structure

```
Project-Pixel-Foolery/
├── LICENSE
├── README.md
├── Notebooks/
│   ├── PURECNN.ipynb
│   ├── RESNET.ipynb
│   └── WITH_ONLY_2_CLASSES_CAT_AND_DOG.ipynb
├── RESULTS/
│   ├── After Updation/
│   │   ├── 1_Pixel.jpg ... 5_Pixels.jpg
│   │   └── README.md
│   ├── PureCNN-MultiClass.png
│   ├── RESNET-MultiClass.png
│   └── README.md
├── REPORTS/
│   ├── BEFORE UPDATION.pdf
│   ├── UPDATED REPORT.pdf
│   └── README.md
├── 2 Classes/
│   ├── WITH_ONLY_2_CLASSES_CAT_AND_DOG.ipynb
│   └── README.md
```

---

## 🔬 Methodology

We use **Differential Evolution (DE)** to optimise pixel positions and RGB values to degrade model confidence:

- **Mutation**: Introduces variation across candidate perturbations
- **Crossover**: Merges candidates for diversity
- **Selection**: Retains perturbations that reduce true-class confidence

All attacks are **black-box**, requiring no access to gradients or model internals.

---

## 🧪 Experimental Results

### 🔹 Pre-Updation (CIFAR-10)

| Model           | Epochs | Accuracy (%) | Pixels Perturbed | True Confidence (Before → After) | Misclassified As | Misclass Confidence | DE Iterations |
|-----------------|--------|--------------|-------------------|----------------------------------|------------------|----------------------|----------------|
| PureCNN         | 100    | 84.63        | 5                 | 0.42 → 0.16                      | Deer             | 0.54                | 100            |
| Modified ResNet | 50     | 81.69        | 5                 | 0.99 → 0.22                      | Dog              | 0.77                | 200            |

### 🔸 Post-Updation (Modified ResNet only)

| Pixels Changed | True Class Confidence | Predicted Class | Predicted Confidence |
|----------------|------------------------|------------------|------------------------|
| 1 pixel        | 0.82 → 0.05            | Dog              | 0.95                   |
| 2 pixels       | 0.82 → 0.02            | Dog              | 0.98                   |
| 3 pixels       | 0.82 → 0.00            | Dog              | 1.00                   |
| 4 pixels       | 0.82 → 0.00            | Dog              | 1.00                   |
| 5 pixels       | 0.82 → 0.00            | Dog              | 1.00                   |

---

## 🧱 Model Architectures

### 📦 PureCNN

```
Input
  ↓
Conv2D(96)
  ↓
Dropout
  ↓
Conv2D(96)
  ↓
Conv2D(96, stride=2)
  ↓
Dropout
  ↓
Conv2D(192)
  ↓
Conv2D(192)
  ↓
Conv2D(192, stride=2)
  ↓
Dropout
  ↓
Conv2D(192)
  ↓
ReLU
  ↓
Conv2D(192)
  ↓
ReLU
  ↓
Conv2D(10)
  ↓
GlobalAveragePooling2D
  ↓
Softmax
```

### 🔁 Modified ResNet

```
Input
  ↓
Conv2D(16) → BN → ReLU
  ↓
[Conv2D(16) → BN → ReLU → Conv2D(16) → BN + Skip → ReLU] × 2
  ↓
[Conv2D(32, stride=2) → BN → ReLU → Conv2D(32) → BN + Skip → ReLU] × 2
  ↓
[Conv2D(64, stride=2) → BN → ReLU → Conv2D(64) → BN + Skip → ReLU] × 2
  ↓
AvgPool
  ↓
Flatten
  ↓
Dense(10)
  ↓
Softmax
```

---

## 👤 Author

**Adarsh Venugopal**  
GitHub: [AVM-27](https://github.com/AVM-27)

---
