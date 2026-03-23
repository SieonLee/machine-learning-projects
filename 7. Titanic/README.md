# Titanic Survival Prediction

## Overview

This project revisits the Titanic dataset as a classification problem, but the interesting part is less the benchmark itself and more the way feature engineering changes what the model can learn.

The notebook uses survival prediction as a chance to work through missing values, family structure, title extraction, and cabin information in a way that keeps the final model interpretable rather than overcomplicated.

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

## EDA Interpretation

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

## Conclusion

The final model reinforces one of the most consistent patterns in the Titanic dataset: survival was strongly shaped by social position and access, not just randomness. Sex and passenger class remain the most important signals, while fare, age, and cabin-related features add useful context around privilege and travel conditions.

From a modeling perspective, logistic regression turned out to be the most balanced final choice. That is a good reminder that a simpler model can still be the right answer when the feature engineering is thoughtful and the problem structure is relatively interpretable.

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- joblib
