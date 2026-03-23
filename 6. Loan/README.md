# Loan Interest Rate Prediction

## Overview

This project predicts loan interest rates from borrower, credit, and application features, but the harder part is not the model itself. It is getting the data into a form that deserves to be modeled in the first place.

Because the dataset contains messy formatting, missing values, and inconsistent fields, the notebook ends up looking much more like a realistic lending workflow than a clean benchmark problem. That is exactly why I wanted it in the portfolio.

## Problem Definition

**Task:** Regression  
**Target Variable:** `X1` (Loan Interest Rate)

### Main Question

Can we accurately estimate loan interest rates using structured loan, borrower, and credit-related features?

## Dataset

- Training data: `Data for Cleaning & Modeling.csv`
- Holdout data: `Holdout for Testing.csv`

The dataset includes application, borrower, credit, and loan pricing fields with intentionally dirty values and missing data.

## Methodology

### 1. Data Cleaning

Several fields required custom cleaning before modeling:

- Converted percentage strings in `X1` into numeric values
- Removed currency formatting from loan amount variables
- Extracted numeric loan term values from text fields
- Standardized numerical columns using type conversion
- Removed identifier columns such as `X2` and `X3`

This step was necessary because the raw dataset simulated real-world messy input data.

### 2. Exploratory Data Analysis

The notebook examines:

- Interest rate distribution
- Relationship between loan grade and interest rate
- Numerical correlation structure
- Missing value patterns
- Outlier behavior across key financial variables

One major finding is that loan grade (`X8`) is the strongest driver of pricing, with average rates increasing consistently from Grade A to Grade G.

### 3. Preprocessing

The modeling pipeline includes:

- Categorical missing value fill with `Missing`
- Median imputation for numerical variables
- Outlier capping using IQR-based bounds from the training set
- Label encoding for categorical variables
- Standard scaling for linear models

### 4. Model Training

Five regression models were compared:

- Random Forest Regressor
- Gradient Boosting Regressor
- Ridge Regression
- Lasso Regression
- ElasticNet

Validation performance was compared using:

- RMSE
- R²
- MAE

## Results

### Model Comparison Summary

- **Random Forest**
  - Achieved the lowest validation RMSE
  - Selected as the final model
  - Best captured non-linear interactions across borrower and loan features

- **Gradient Boosting**
  - Performed competitively
  - Strong predictive potential, but more sensitive to tuning and overfitting

- **Ridge / Lasso / ElasticNet**
  - Faster and more interpretable
  - Weaker predictive accuracy, suggesting that a purely linear relationship is insufficient for this dataset

### Final Model Choice

Random Forest was selected as the final model because it delivered the strongest validation performance and handled complex feature interactions more effectively than the linear baselines.

## Conclusion

The main takeaway from this project is that loan pricing behaves like a messy real-world regression problem rather than a clean classroom dataset. A large part of the work lies in cleaning inconsistent fields, handling missing values, and building a pipeline that can score new data reliably. Once that foundation is in place, the modeling results show that nonlinear methods are better suited than linear baselines for capturing how borrower and loan characteristics combine to determine interest rates.

Loan grade stands out as the strongest pricing signal, which aligns with how lending decisions are typically structured. That makes the final model behavior easy to justify: the algorithm is not uncovering something mysterious, but learning a hierarchy that already exists in credit pricing.

## Deployment Workflow

This project includes a practical scoring workflow:

- Save trained models with `joblib`
- Save supporting preprocessing objects such as scalers and mappings
- Reload the best model
- Apply the same cleaning and preprocessing logic to the holdout dataset
- Export final predictions to `Results from sieonlee.csv`

This makes the notebook closer to a reusable applied ML workflow than a one-off regression exercise.

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- joblib
