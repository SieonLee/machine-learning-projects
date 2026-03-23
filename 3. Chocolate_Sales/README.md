# Chocolate Sales Analysis & Revenue Prediction

## Overview

This project looks at chocolate sales data to understand what is actually driving revenue and how much of that story a regression model can capture.

What I like about this dataset is that it pushes past the easy assumption that selling more boxes should always mean making more money. Once pricing differences across products enter the picture, revenue becomes a much more interesting variable to analyze.

---

## Dataset

The dataset contains 3,282 sales transactions with the following columns:

- Sales Person – Sales representative
- Country – Sales region
- Product – Chocolate product type
- Date – Transaction date
- Amount – Revenue (string formatted with $ and commas)
- Boxes Shipped – Number of boxes sold

---

## Methodology

### 1. Data Cleaning

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

### 2. Exploratory Data Analysis

Key findings from EDA:

- The overall correlation between Amount and Boxes Shipped is near zero.  
  This indicates revenue is not purely volume-driven. Product pricing variation significantly affects revenue.

- Pareto analysis shows that a small number of products contribute disproportionately to total revenue.

- Clear pricing structure differences exist between product categories.

- Monthly sales trends indicate seasonal fluctuations.

---

### 3. Modeling Approach

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

### 4. Models Evaluated

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

## Results

- Tree-based models outperform linear regression.
- Random Forest achieves the best predictive performance.
- Product category and Boxes Shipped are the strongest predictors of revenue.
- Revenue is more influenced by pricing structure than volume alone.

---

## Conclusion

The strongest theme in this analysis is that chocolate revenue is shaped by product mix and pricing structure much more than by shipment volume alone. That is why the overall relationship between `Amount` and `Boxes Shipped` stays weaker than a simple sales intuition might suggest. Selling more units matters, but what is being sold matters just as much.

The modeling results support that story. Tree-based methods outperform linear regression because the problem contains product-specific and regional interactions that are hard to represent with a single linear relationship. In practice, this makes the project more valuable as a business analysis of pricing and sales structure than as a narrow prediction exercise.

---

## Tech Stack

- Python
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
