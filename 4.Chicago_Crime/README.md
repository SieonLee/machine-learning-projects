# Chicago Crime Arrest Prediction (Time-Aware Modeling)

## Project Overview

This project aims to predict whether an arrest will be made given historical crime records from the Chicago Crime dataset.

Instead of using a naive random split, this analysis applies a time-aware training strategy to simulate real-world deployment and prevent temporal data leakage.

The objective is not only predictive performance, but also to demonstrate practical data science considerations such as:

- Temporal drift
- Class imbalance handling
- Model comparison (linear vs non-linear)
- Deployment-aware validation strategy
- Ethical awareness in predictive modeling

---

## Problem Definition

Task: Binary Classification  
Target Variable: `Arrest` (1 = Arrest Made, 0 = No Arrest)

Main Question:

Can we predict the probability of an arrest based on crime type, time, and location features?

---

## Dataset

- Source: Chicago Crime Dataset (2000–2025)
- Filtered to: Most recent 10 years
- Final size:
  - Train: ~1.98M rows
  - Test: ~0.26M rows
- Arrest rate: ~16% (class imbalance)

To ensure temporal relevance and reduce concept drift, only the most recent decade was used for modeling.

---

## Methodology

### 1. Data Preprocessing

- Removed high-missing or leakage-prone columns
- Extracted temporal features:
  - Hour
  - DayOfWeek
- Selected key predictors:
  - Primary Type
  - Location Description
  - District
  - Hour
  - DayOfWeek
  - Domestic

Categorical variables were encoded using One-Hot Encoding.

---

### 2. Time-Based Train/Test Split

To simulate a real-world deployment scenario:

- Training data: Earlier years within the last decade
- Test data: Most recent 2 years

This prevents future information leakage and reflects how a model would perform in production.

---

### 3. Handling Class Imbalance

- Arrest rate ≈ 16%
- Primary evaluation metric: ROC-AUC
- Additional metrics:
  - PR-AUC (Average Precision)
  - F1-score

For XGBoost, `scale_pos_weight` was used to address imbalance.

---

## Models

| Model | Purpose |
|--------|----------|
| Logistic Regression | Baseline, interpretability |
| XGBoost | Non-linear modeling and performance improvement |

---

## Results

| Model | ROC-AUC | PR-AUC | F1-score |
|--------|----------|----------|----------|
| Logistic Regression | ~0.84 | See notebook | See notebook |
| XGBoost | See notebook | See notebook | See notebook |

### Key Observations

- Logistic Regression achieved strong baseline performance (ROC-AUC ≈ 0.84), indicating strong structural relationships between crime type and arrest outcomes.
- XGBoost captured additional non-linear interactions and improved predictive performance.
- Arrest probability varies significantly by:
  - Crime type
  - Time of day
  - District

---

## Insights from EDA

- Arrest rates show clear hourly patterns, with higher rates in the morning and evening.
- A significant drop in arrest rate was observed around 2020–2022, followed by partial recovery.
- Certain crime categories show near-deterministic arrest outcomes, indicating strong structural patterns in the data.

---

## Limitations and Ethical Considerations

- Arrest outcomes may reflect systemic policing practices rather than purely crime severity.
- Temporal drift observed after 2020 suggests that periodic retraining would be necessary in a real deployment setting.
- Predictive models in policing contexts require careful monitoring for bias and fairness risks.


---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- XGBoost
- matplotlib
- seaborn

---

## Summary

This project demonstrates:

- Time-aware modeling to prevent data leakage
- Practical handling of class imbalance
- Baseline versus advanced model comparison
- Realistic deployment considerations
- Awareness of ethical risks in predictive modeling
