# Chocolate Sales Analysis & Revenue Prediction

## Overview

This project analyzes a chocolate sales dataset to uncover business insights and build a regression model to predict revenue (`Amount`).

The analysis follows a structured data science workflow:

1. Exploratory Data Analysis (EDA)
2. Feature Engineering
3. Regression Modeling
4. Model Evaluation and Interpretation

The objective is not only to build a predictive model, but also to understand revenue structure and identify key sales drivers.

---

## Dataset Description

The dataset contains 3,282 sales transactions with the following columns:

- Sales Person – Sales representative
- Country – Sales region
- Product – Chocolate product type
- Date – Transaction date
- Amount – Revenue (string formatted with $ and commas)
- Boxes Shipped – Number of boxes sold

---

## Data Cleaning

- Converted `Amount` from string (e.g., "$1,200") to float
- Converted `Date` to datetime format
- Verified absence of missing values
- Generated time-based features:
  - Year
  - Month
  - Day
  - DayOfWeek
  - WeekOfYear
- Created derived feature:
  - `Price_per_box = Amount / Boxes Shipped`

---

## Exploratory Data Analysis

Key findings from EDA:

- The overall correlation between Amount and Boxes Shipped is near zero.  
  This indicates revenue is not purely volume-driven. Product pricing variation significantly affects revenue.

- Pareto analysis shows that a small number of products contribute disproportionately to total revenue.

- Clear pricing structure differences exist between product categories.

- Monthly sales trends indicate seasonal fluctuations.

---

## Modeling Approach

### Problem Definition

Regression Task  
Target Variable: `Amount` (Revenue)

### Features Used

- Sales Person
- Country
- Product
- Boxes Shipped
- Year
- Month
- Day
- DayOfWeek
- WeekOfYear

Categorical variables were encoded using One-Hot Encoding.

---

## Models Evaluated

1. Baseline Model (Mean prediction)
2. Ridge Regression
3. Decision Tree Regressor
4. Random Forest Regressor

### Evaluation Metrics

- RMSE (Root Mean Squared Error)
- MAE (Mean Absolute Error)
- R² Score

Cross-validation was applied to ensure robustness.

---

## Results Summary

- Tree-based models outperform linear regression.
- Random Forest achieves the best predictive performance.
- Product category and Boxes Shipped are the strongest predictors of revenue.
- Revenue is more influenced by pricing structure than volume alone.

---

## Key Insights

- Revenue is not linearly driven by volume.
- A small subset of products generates the majority of total sales (Pareto effect).
- Product pricing structure plays a dominant role in revenue prediction.
- Sales performance varies significantly by product and region.

---

## Tech Stack

- Python
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
