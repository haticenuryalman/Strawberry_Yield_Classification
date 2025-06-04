# Strawberry Yield Classification using Support Vector Machines (SVM)

This repository presents a machine learning-based approach for classifying strawberry yield and cultivar types using the Support Vector Machines (SVM) algorithm. The project is built upon a structured agricultural dataset published by Luraschi et al. (2024), aimed at understanding the effect of biostimulant treatments on fruit yield and quality.

---

## 📌 Project Overview

- **Title**: Classification of Strawberry Yield Using Machine Learning Techniques
- **Dataset Source**: [Luraschi et al., 2024 - Data in Brief](https://www.sciencedirect.com/science/article/pii/S2352340925001775)

The primary goal of this project is to assess whether fruit yield levels and cultivar types can be predicted based on numerical agronomic data through SVM classifiers.

---

## 🧪 Dataset Description

The dataset consists of measurements from controlled experiments evaluating the effects of different biostimulant products and dosages on strawberry plants. Each row represents a treatment combination and includes:

- Total and commercial fruit count
- Fresh fruit weight (g)
- Commercial yield (kg/m²)
- Fruit diameter and length (cm)
- Firmness (kgf/cm³)
- Total soluble solids (°Brix)
- pH, titratable acidity, etc.

### Labeling Scenarios
1. **Binary Yield Classification**: Samples labeled as *High* or *Low* based on the median commercial yield.
2. **Multi-Class Variety Classification**: Samples labeled as V1–V7 based on cultivar codes extracted from treatment identifiers.

---

## 🔧 Data Preprocessing

- Removed unnamed or irrelevant columns
- Standardized decimal separators (comma to dot) and converted to float
- Cleaned treatment names (removed asterisks and whitespaces)
- **Normalization**: StandardScaler (mean = 0, std = 1) to ensure SVM performance
- **Train/Test Split**: 70% training, 30% testing

---

## 📚 Machine Learning Approach

### Algorithm
- **Model**: Support Vector Machines (SVM)
- **Kernel**: RBF (Radial Basis Function)
- **C**: 1.0 (default)
- **Gamma**: 'scale' (default)

Separate models were trained for each classification scenario.

### GridSearchCV Tuning
A hyperparameter search using 5-fold cross-validation was conducted. Best results:
- Kernel: **linear**
- C: **10**
- Gamma: **scale**
- Cross-validation accuracy: **97.65%**

---

## 📊 Evaluation and Results

### Scenario 1: High–Low Yield Classification
- **Accuracy**: 100%
- **ROC AUC**: 1.00
- **Confusion Matrix**: Perfect separation between classes

> ⚠️ Caution: While the model achieved perfect results, this may be due to an overly simple dataset structure or overfitting.

### Scenario 2: Cultivar (V1–V7) Classification
- **Accuracy**: 54%
- **Observation**:
  - Some classes (e.g., V4, V6) not predicted at all
  - Overlapping measurements between classes (e.g., V2, V3, V7) led to misclassifications
  - Small sample sizes and class imbalance negatively affected generalizability

---

## 🔍 Comparative Analysis

| Feature              | Luraschi et al. | Zydlik et al. | This Project (SVM)         |
|----------------------|------------------|----------------|-----------------------------|
| Methodology          | ANOVA / Mean     | ANOVA / LSD    | SVM + GridSearchCV         |
| Focus                | Yield and quality| Variety yield  | Predictive classification  |
| Predictive Modeling  | No               | No             | Yes                         |
| Key Performance      | -                | -              | Accuracy (0.54–1.00), AUC=1 |
| Best Varieties       | V1–V5            | V1, V5         | V1, V5 classified well      |
| Biostimulant Effect  | Descriptive      | Descriptive    | Linked to yield classes     |

---

## ✅ Conclusions

- SVM is highly effective when class boundaries are clear and well-separated.
- Performance degrades significantly in imbalanced, overlapping multi-class scenarios.
- Hyperparameter tuning via GridSearchCV boosts model reliability.
- Further improvement could be achieved using ensemble models (Random Forest, XGBoost).

---

## 🔮 Recommendations for Future Work

- Expand the dataset with more samples and regional diversity.
- Apply class balancing techniques (e.g., SMOTE, undersampling).
- Try alternative classifiers: Random Forest, Logistic Regression, XGBoost.
- Use dimensionality reduction (e.g., PCA) to improve model robustness.

---

## 🛠️ How to Run

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Launch the notebook:
```bash
jupyter notebook Untitled.ipynb
```

---

## 📖 References

- [Luraschi et al., 2024 - Data in Brief](https://www.sciencedirect.com/science/article/pii/S2352340925001775)
- [Zydlik et al., 2024 - Agronomy](https://www.mdpi.com/2073-4395/14/8/1786)
