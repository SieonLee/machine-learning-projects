# Student Exam Score Prediction & Factor Analysis

## Project Overview

This project analyzes the key factors influencing students' exam scores and builds predictive models to quantify their impact.

The focus is not only on model performance but also on:

- Data leakage detection
- Multicollinearity handling
- Model interpretability
- Reproducibility

---

## Problem Statement

**Goal:**  
Identify the most important variables affecting `exam_score` and build a reliable predictive model.

Key Questions:

- Which variables significantly impact exam performance?
- Is there multicollinearity?
- Is there data leakage?
- Which variables are actionable from a policy perspective?

---

## Data Preprocessing

### 1. Numeric Feature Selection

Only numerical variables were used for correlation and regression analysis.

### 2. Data Leakage Detection

Initial modeling produced:

- Linear Regression R² = 1.0  
- Random Forest R² ≈ 0.9999  

This indicated severe data leakage.

Highly correlated variables:

- `productivity_score`
- `focus_index`

These variables were likely intermediate or derived features directly related to `exam_score`.  
They were removed before final modeling.

### 3. Multicollinearity Check (VIF)

Variance Inflation Factor (VIF) was computed.

- `productivity_score` showed VIF > 10 and was removed.
- `student_id` was removed as a non-informative identifier.

---

## Modeling Approach

### Train/Test Split

- 80 / 20 split
- Fixed random state for reproducibility

### 1. Linear Regression

- Standardized features using `StandardScaler`
- Evaluated using R² and RMSE
- Used primarily for interpretability

### 2. Random Forest Regressor

- Captured non-linear relationships
- Used for feature importance comparison

---

## Final Model Performance (After Fixing Leakage)

Linear Regression:

- R²: 0.739  
- RMSE: 5.96  

The model explains approximately 74% of the variance in exam scores, which is realistic for behavioral data.

---

## Key Findings

Top influential variables (based on standardized coefficients):

| Feature               | Impact            |
|-----------------------|------------------|
| mental_health_score   | Strong positive  |
| study_hours           | Strong positive  |
| burnout_level         | Strong negative  |
| social_media_hours    | Moderate negative|
| sleep_hours           | Mild positive    |

### Interpretation

- Better mental health significantly improves exam performance.
- Increased study hours strongly increase exam scores.
- Burnout negatively impacts academic performance.
- Social media usage slightly reduces performance.
- Sleep has a modest positive effect.

---

## Practical Implications

From a policy perspective:

- Investing in student mental health support may significantly improve academic outcomes.
- Burnout management is critical for sustained performance.
- Encouraging structured study habits is effective.
- Reducing digital distractions may provide moderate improvements.

---

## Lessons Learned

- Detecting and removing data leakage is critical.
- High R² can indicate leakage rather than strong modeling.
- Multicollinearity must be handled before interpreting coefficients.
- Comparing linear and non-linear models provides deeper insight.
- Proper train/test separation ensures realistic evaluation.

---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- statsmodels
- matplotlib
- seaborn

---

## Interview Explanation

Initially, the model achieved R² = 1.0, which indicated data leakage.  
After identifying and removing highly correlated intermediate variables, the final model achieved a realistic R² of 0.74.  
The analysis revealed that mental health, study hours, and burnout are the strongest predictors of exam performance.
