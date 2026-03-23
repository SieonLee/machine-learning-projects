# Heart Disease Risk Prediction From Scratch

## Overview

This project predicts heart disease risk using a public Kaggle dataset, but the real purpose is to show the mechanics behind a core classification model rather than only relying on library defaults.

I wanted this notebook to feel like a bridge between fundamentals and applied work. It uses a real dataset, but the model itself is implemented from scratch so the workflow still says something about how the algorithm actually works under the hood.

---

## Problem Definition

**Task:** Binary classification  
**Target Variable:** `HeartDisease`

### Main Questions

- Can a from-scratch logistic regression model perform competitively on a real Kaggle dataset?
- Which patient features appear most associated with elevated heart disease risk?
- How close is the custom implementation to a library baseline?

---

## Dataset

This project uses the [Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction) from Kaggle.

- 918 rows
- 11 input features
- 1 binary target

### Key Variables

- `Age`
- `Sex`
- `ChestPainType`
- `RestingBP`
- `Cholesterol`
- `FastingBS`
- `RestingECG`
- `MaxHR`
- `ExerciseAngina`
- `Oldpeak`
- `ST_Slope`
- `HeartDisease`

The target distribution is moderately balanced:

- No heart disease: 410
- Heart disease: 508

---

## Methodology

### 1. Exploratory Data Analysis

- reviewed target balance
- profiled numeric variables such as age, resting blood pressure, cholesterol, and max heart rate
- compared feature distributions across positive and negative heart disease cases

### 2. Preprocessing

- one-hot encoded categorical features
- standardized the design matrix using training-set statistics only
- used a stratified train/test split

### 3. Logistic Regression From Scratch

The notebook includes a custom implementation of logistic regression using:

- batch gradient descent
- sigmoid activation
- binary cross-entropy loss
- L2 regularization

### 4. Baseline Comparison

To validate the custom implementation, the project compares it against scikit-learn's `LogisticRegression` on the same train/test split.

---

## Results

### Test Set Performance

- Logistic Regression (Scratch)
  - Accuracy: 0.8859
  - Precision: 0.8716
  - Recall: 0.9314
  - F1 Score: 0.9005
  - ROC AUC: 0.9292

- Logistic Regression (scikit-learn)
  - Accuracy: 0.8859
  - Precision: 0.8716
  - Recall: 0.9314
  - F1 Score: 0.9005
  - ROC AUC: 0.9297

## Graph Interpretation

The exploratory plots suggest that the positive class is not driven by a single lab-style measurement. Instead, the clearer separation comes from a combination of clinical context and exercise-related features.

Patients labeled with heart disease tend to be older on average and show lower maximum heart rate during exercise. The chest pain plot is especially informative: asymptomatic chest pain appears much more often in positive cases, while more typical angina patterns are relatively more common in negative cases. Cholesterol and resting blood pressure vary across both groups, but they do not separate the classes as cleanly on their own.

The coefficient plot tells a similar story. Features tied to chest pain type, ST slope, and exercise-induced angina carry some of the strongest weights, which suggests that the model is learning a clinically plausible boundary rather than memorizing noise from one numeric column.

---

## Conclusion

The main conclusion from this notebook is that a relatively simple classifier is already strong enough to capture most of the useful signal in this dataset. The from-scratch logistic regression model reaches nearly identical performance to scikit-learn, which is a good sign that the implementation is correct and that the problem itself is well suited to a linear probabilistic model.

The confusion matrix also helps frame the result in a more practical way. On the held-out test set, the model correctly identifies most heart disease cases and misses relatively few positives, which is why recall is high at 0.9314. That tradeoff leads to some false positives, but for a screening-style setting that is often more acceptable than missing high-risk patients.

Overall, this project works well as both a fundamentals exercise and a portfolio piece. It shows that core machine learning ideas like gradient descent, logistic loss, and coefficient interpretation can be implemented from scratch while still producing results that are useful, interpretable, and close to production-grade library behavior.

---

## Expected Outputs

- target distribution summary
- exploratory plots for major clinical variables
- training loss curve for the custom model
- scratch vs baseline comparison table
- confusion matrix and classification report
- coefficient interpretation

---

## Why This Project Matters

This project strengthens the portfolio in a way that standard notebook projects often do not. It shows not only that I can apply machine learning to a business or health-style dataset, but also that I understand the mechanics behind a core classification algorithm.

It complements the rest of the repository by adding:

- algorithmic understanding, not just model usage
- custom numerical optimization in NumPy
- interpretable classification on a real Kaggle dataset
- a cleaner bridge between theory and applied portfolio work

---

## Tech Stack

- Python
- NumPy
- pandas
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook

---

## Files

- `heart_disease_from_scratch.ipynb` - main notebook
- `data/heart.csv` - local Kaggle dataset copy used by the notebook
