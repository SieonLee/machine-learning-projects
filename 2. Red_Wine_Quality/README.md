# Red Wine Quality Classification

A machine learning project that predicts whether a red wine is high quality based on its physicochemical properties.  
This project emphasizes structured experimentation, generalization performance, and model interpretability rather than accuracy alone.

---

## Project Overview

This project uses the UCI Red Wine Quality dataset to build a binary classification model that predicts high-quality wines.

- **Original Target:** `quality (0–10)`
- **Binary Target**
  - `1 (Good)` → quality ≥ 7  
  - `0 (Not Good)` → quality < 7  

**Modeling pipeline:**  
Baseline → Performance Improvement → Cross Validation → Interpretation → Error Analysis

---

## Problem Definition

### Objective
To classify whether a wine is high quality (quality ≥ 7) using its chemical characteristics.

### Task Type
Supervised Learning – Binary Classification

### Evaluation Metrics

- Accuracy
- F1-score
- ROC-AUC
- PR-AUC

Special attention was given to F1-score and PR-AUC due to class imbalance.

---

## Dataset

- **Source:** UCI Red Wine Quality Dataset
- **Samples:** 1,599
- **Features:** 11 continuous physicochemical variables

### Key Features

- alcohol
- volatile acidity
- sulphates
- citric acid
- residual sugar

---

## Modeling Approach

### 1. Data Preprocessing

- Binary target engineering (quality ≥ 7)
- Stratified train/test split
- StandardScaler for Logistic Regression
- Random seed fixed for reproducibility

---

### 2. Baseline Model – Logistic Regression

- Confusion matrix analysis
- ROC-AUC and PR-AUC evaluation
- Threshold tuning
- Class imbalance handling using `class_weight="balanced"`

---

### 3. Ensemble Model – Random Forest

- Stratified 5-fold Cross Validation
- Hyperparameter tuning via GridSearchCV
- Model selection based on F1-score

---

### 4. Model Interpretation

- Feature Importance
- Permutation Importance

Top influential features:

- alcohol
- sulphates
- volatile acidity

---

### 5. Error Analysis

- False Negative analysis
- False Positive analysis
- Misclassification pattern inspection

---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn

