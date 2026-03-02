# Titanic Survival Prediction

## Project Overview

This project predicts whether a Titanic passenger survived using structured passenger information such as class, sex, age, fare, embarkation port, and family-related features.

The objective is not only to build a classification model, but also to demonstrate practical machine learning workflow elements such as:

- Missing value analysis
- Feature engineering
- Class imbalance awareness
- Model comparison
- Model saving and reloading for holdout prediction

## Problem Definition

**Task:** Binary Classification  
**Target Variable:** `Survived` (1 = Survived, 0 = Did Not Survive)

### Main Question

Can we predict passenger survival using demographic, socioeconomic, and travel-related features?

## Dataset

- Training data: `train.csv`
- Holdout data: `holdout_test.csv`

### Core Features

- `Pclass`
- `Sex`
- `Age`
- `Fare`
- `Embarked`
- `SibSp`
- `Parch`

## Methodology

### 1. Data Preprocessing

- Removed identifier-only variables such as `PassengerId`
- Investigated missing values in `Age`, `Cabin`, and `Embarked`
- Filled `Embarked` with the most common category
- Imputed `Age` using median age by passenger title
- Converted cabin information into more useful engineered features

### 2. Feature Engineering

Additional features were created to improve predictive performance:

- `Title` extracted from passenger names
- `HasCabin`
- `Cabin_letter`
- `Age_Missing`
- `FamilySize`
- `IsAlone`

These features help capture hidden survival patterns related to social status, documentation quality, and travel context.

### 3. Class Imbalance Handling

The notebook checks the class distribution and uses `class_weight="balanced"` in several models to improve handling of survival imbalance.

### 4. Model Training

Categorical variables were one-hot encoded and numerical variables were scaled using a preprocessing pipeline.

The following models were compared:

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting

## Results

### Model Comparison Summary

- **Logistic Regression**
  - Accuracy: 0.821
  - Strong overall balance across precision, recall, and F1-score
  - Selected as the final model

- **Decision Tree**
  - Highest recall
  - More likely to identify survivors, but with weaker precision and greater overfitting risk

- **Random Forest**
  - More stable than a single decision tree
  - Competitive performance, but slightly weaker than Logistic Regression overall

- **Gradient Boosting**
  - Highest precision
  - Strong at correctly predicting survivors, but with lower recall

### Final Model Choice

Logistic Regression was selected as the final model because it achieved the best overall tradeoff between accuracy, precision, recall, and F1-score while remaining interpretable and efficient.

## Insights from EDA

- Female passengers had much higher survival rates than male passengers
- First-class passengers had substantially higher survival rates than third-class passengers
- Younger passengers had somewhat higher survival rates, but age was less influential than sex and class
- Higher fares were associated with higher survival probability
- Missing cabin and age information appeared to carry useful socioeconomic signal

These findings are consistent with historical patterns such as evacuation priority and unequal access to lifeboats.

## Deployment Workflow

This project includes a practical prediction workflow:

- Train and save each model using `joblib`
- Reload the best-performing model
- Apply the same preprocessing logic to a holdout dataset
- Export final predictions to a submission file

This makes the notebook closer to a reusable machine learning pipeline rather than a one-time analysis.

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- joblib

## Summary

This project demonstrates:

- End-to-end binary classification workflow
- Practical feature engineering on tabular data
- Handling of informative missing values
- Comparison of multiple classification models
- Model persistence and holdout prediction workflow
