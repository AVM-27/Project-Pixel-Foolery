# 🧠 Project Pixel Foolery: Fooling Neural Networks with Few-Pixel Attacks

![Status](https://img.shields.io/badge/status-complete-success)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Frameworks](https://img.shields.io/badge/Frameworks-TensorFlow%20%7C%20Keras-orange)
![License](https://img.shields.io/badge/License-MIT-green)

This project explores the fascinating vulnerability of deep convolutional neural networks (CNNs) to adversarial attacks at the pixel level. We demonstrate that it's possible to fool well-trained models by perturbing just **1 to 5 pixels** in an image, forcing them to misclassify with high confidence.

---

## 👥 The Research Team

This project was a collaborative effort by:
* **Anjana C V** `[CB.EN.U4ECE22003]`
* **Adarsh Venugopal** `[CB.EN.U4ECE22004]`
* **Harini K** `[CB.EN.U4ECE22026]`
* **Vikas P K** `[CB.EN.U4ECE22237]`

---

## 🎯 Project Goal

The primary objective is to perform **black-box adversarial attacks** on pre-trained CNN models (**PureCNN** and **Modified ResNet**) using **Differential Evolution (DE)**. The goal is to alter a minimal number of pixels (1-5) to achieve two outcomes:
1.  Drastically reduce the model's confidence in the true class.
2.  Induce a confident misclassification into a different class.

---

## 🔬 Methodology

Our attack strategy is entirely **black-box**, meaning we do not require any knowledge of the model's internal architecture, parameters, or gradients. We use **Differential Evolution (DE)**, a powerful population-based optimization algorithm, to find the optimal pixel perturbations.

The DE algorithm iteratively refines a population of candidate solutions (pixel perturbations) through three main steps:
1.  **🧬 Mutation:** Creates new candidate solutions by adding weighted differences between existing solutions, introducing variation.
2.  **🔄 Crossover:** Combines parameters from the mutated candidates and the original population to increase diversity.
3.  **🏆 Selection:** Compares the new candidates to the original ones and keeps only those that are more "fit"—in our case, those that most successfully reduce the true class's prediction confidence.

---

## 🧪 Experimental Results

We tested our attack on models trained on the **CIFAR-10** dataset and a binary subset (**Cat vs. Dog**). The results clearly show the models' vulnerability.

### 🔹 Pre-Updation (CIFAR-10 Multi-Class)

| Model | Epochs | Accuracy (%) | Pixels Perturbed | True Confidence (Before → After) | Misclassified As | Misclass. Confidence | DE Iterations |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **PureCNN** | 100 | 84.63 | 5 | 0.42 → 0.16 | `Deer` | 0.54 | 100 |
| **Modified ResNet** | 50 | 81.69 | 5 | 0.99 → 0.22 | `Dog` | 0.77 | 200 |

### 🔸 Post-Updation (Modified ResNet on a Cat Image)

The attacks on the updated ResNet model were exceptionally successful, causing confident misclassifications with incredibly few pixels.

| Pixels Changed | True Class Confidence (Cat) | Predicted Class | Predicted Confidence |
| :---: | :---: | :---: | :---: |
| **1 pixel** | 0.82 → **0.05** | `Dog` | **0.95** |
| **2 pixels** | 0.82 → **0.02** | `Dog` | **0.98** |
| **3 pixels** | 0.82 → **0.00** | `Dog` | **1.00** |
| **4 pixels** | 0.82 → **0.00** | `Dog` | **1.00** |
| **5 pixels** | 0.82 → **0.00** | `Dog` | **1.00** |

#### Visual Result (Example with 5 pixels)
![5 Pixel Attack](RESULTS/After%20Updation/5_Pixels.jpg)
*An original image of a cat is misclassified as a dog with 100% confidence after altering just 5 pixels.*

---

## 🧱 Model Architectures

### 📦 PureCNN

A custom-built CNN with multiple convolutional and dropout layers, designed for CIFAR-10.
