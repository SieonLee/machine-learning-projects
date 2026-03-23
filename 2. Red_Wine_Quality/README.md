# Red Wine Quality Classification

This project predicts whether a red wine should be treated as high quality using its physicochemical properties.

It is a relatively compact classification problem, but a useful one for showing how I usually work: define a practical target, evaluate more than one model, and pay attention to where the model is confident versus where the classes are genuinely hard to separate.

---

## Overview

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

## Methodology

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

## Results

The modeling workflow showed that wine quality can be predicted reasonably well from physicochemical measurements, especially once the class imbalance is handled carefully and the baseline is compared against a stronger ensemble model.

Alcohol, sulphates, and volatile acidity consistently appeared as the most influential variables. The random forest also helped capture interactions that a simple linear decision boundary would miss, which is why it served as a stronger final model for this problem.

## Conclusion

This project works well as a compact classification case study because it combines preprocessing, imbalance-aware evaluation, model comparison, and interpretation in a clean notebook workflow. The main conclusion is that wine quality is meaningfully predictable, but not perfectly separable. That ambiguity is part of what makes the dataset useful: the signal is real, yet still complex enough to reward careful modeling rather than a single simple rule.

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
