# Student Exam Score Prediction & Factor Analysis

## Overview

This project looks at student performance data with a simple question in mind: what actually seems to move exam scores, and which relationships still look believable once the easy sources of leakage are removed?

What makes the notebook interesting is that the first version of the model looks unrealistically good. That turns the project into more than a regression exercise. It becomes a small example of the kind of skepticism data science often requires before any result is worth interpreting.

---

## Problem Definition

**Task:** Regression  
**Target Variable:** `exam_score`

### Main Questions

- Which variables are most strongly associated with exam performance?
- Are any features leaking target information into the model?
- Is multicollinearity affecting interpretability?
- Which findings are potentially actionable from a policy or student-support perspective?

---

## Dataset

This project uses a student performance dataset with academic, behavioral, and well-being related features.

### Example Variables

- `study_hours`
- `mental_health_score`
- `burnout_level`
- `sleep_hours`
- `social_media_hours`
- `attendance_percentage`
- `exam_score`

The analysis focuses on predicting `exam_score` while separating useful explanatory variables from features that create unrealistic performance.

---

## Methodology

### 1. Leakage Detection

The initial models produced near-perfect performance:

- Linear Regression R² = 1.0
- Random Forest R² ≈ 0.9999

This was a strong sign of target leakage rather than genuine predictive power.

Highly correlated variables such as `productivity_score` and `focus_index` appeared to behave like intermediate or derived versions of the target and were removed before final modeling.

### 2. Multicollinearity Check

Variance Inflation Factor (VIF) was used to inspect redundancy among predictors.

- `productivity_score` showed very high VIF and was removed
- `student_id` was dropped as a non-informative identifier

### 3. Modeling

The final workflow uses an 80/20 train/test split with a fixed random state.

Models compared:

- Linear Regression with `StandardScaler`
- Random Forest Regressor for nonlinear comparison

The linear model is used mainly for interpretability, while the random forest helps check whether nonlinear structure adds additional predictive value.

---

## Results

### Final Model Performance After Leakage Removal

- Linear Regression
  - R²: 0.739
  - RMSE: 5.96

The post-cleaning performance is much more realistic and therefore more trustworthy than the original near-perfect scores.

### Interpretation

The final model suggests that exam performance is shaped by a combination of effort, well-being, and sustainable habits rather than any single feature.

The strongest positive signals come from mental health and study hours, while burnout shows a clear negative relationship with exam score. Social media usage also appears negatively related to performance, though its effect is more moderate. Sleep contributes positively, but in this dataset it seems less influential than study behavior and emotional well-being.

---

## Conclusion

The most important outcome of this project is not the exact R² value, but the fact that the model became believable once leakage was removed. That shift matters because it turns the notebook from a misleading high-score exercise into a credible analysis of student performance.

The broader conclusion is that academic outcomes in this dataset appear closely tied to mental health, structured study time, and burnout management. In other words, performance looks less like a pure intelligence or effort problem and more like a balance of discipline, support, and sustainability.

This makes the project useful both as a modeling exercise and as an example of analytical judgment. Detecting unrealistic results, questioning them, and rebuilding the workflow carefully is part of the work, not a side note.

---

## Practical Implications

- mental health support may improve academic outcomes more than simple short-term performance pressure
- burnout reduction is likely important for sustained performance
- structured study habits appear more valuable than just increasing activity without focus
- reducing digital distraction may offer modest gains when combined with broader support factors

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

## Interview Summary

This project started with unrealistically strong model performance, which led to a leakage investigation. After removing target-like features and checking multicollinearity, the final regression model achieved a more realistic R² of 0.739. The cleaned analysis showed that mental health, study hours, and burnout were among the strongest factors associated with exam performance.
