# Bike Demand Forecasting

## Overview

This project predicts bike rental demand using time-based and weather-related features.

The goal is to build a practical forecasting workflow that combines exploratory data analysis, temporal feature engineering, and regression modeling in a format consistent with the rest of my machine learning project portfolio.

This project focuses on:

- time-based exploratory data analysis
- temporal and seasonal feature engineering
- regression modeling for demand prediction
- time-aware evaluation for realistic forecasting performance

---

## Problem Definition

**Task:** Time Series Regression  
**Target Variable:** `cnt`

### Main Questions

- Can we predict bike rental demand using historical time and weather information?
- Which temporal features are most important for forecasting rental volume?
- How much improvement do lag-based features provide over a simple baseline model?

---

## Dataset

This project uses the hourly Bike Sharing Dataset from the UCI Machine Learning Repository.

Main variables used in this project include:

- `dteday`
- `hr`
- `season`
- `yr`
- `mnth`
- `holiday`
- `workingday`
- `weathersit`
- `temp`
- `atemp`
- `hum`
- `windspeed`
- `cnt`

The dataset is well suited for this project because it combines seasonal patterns, hourly demand behavior, and weather effects in a structured tabular format.

---

## Methodology

### 1. Exploratory Data Analysis

- Analyze the distribution of bike demand
- Visualize hourly, daily, and monthly usage patterns
- Examine how weather and temperature affect demand
- Check for missing values, duplicates, and outliers

### 2. Feature Engineering

To capture temporal structure, the following features are created:

- `year`
- `month`
- `day`
- `hour`
- `weekday`
- `is_weekend`

Lag and rolling features are also created to improve forecasting performance:

- `lag_1`
- `lag_24`
- `lag_168`
- `rolling_mean_24`
- `rolling_std_24`

### 3. Model Training

The workflow compares:

- Linear Regression as a simple baseline
- Random Forest Regressor
- Gradient Boosting Regressor

### 4. Time-Aware Evaluation

Instead of using random train-test splitting, the data is split chronologically to better simulate real forecasting conditions and reduce leakage risk.

---

## Results

The final model comparison showed that tree-based ensemble models outperformed the linear baseline for bike demand forecasting.

### Model Performance

- Linear Regression
  - MAE: 60.96
  - RMSE: 89.15
  - R²: 0.8355

- Random Forest Regressor
  - MAE: 33.93
  - RMSE: 57.70
  - R²: 0.9311

- Gradient Boosting Regressor
  - MAE: 34.14
  - RMSE: 52.79
  - R²: 0.9423

### Key Findings

- Tree-based ensemble models performed substantially better than the linear baseline.
- Gradient Boosting achieved the best overall performance, with the highest R² and lowest RMSE.
- Random Forest also performed strongly and produced the lowest MAE among the tree-based models by a small margin.
- Lag and rolling features contributed meaningful predictive signal by capturing short-term temporal dependence.
- Time-aware validation provided a realistic estimate of forecasting performance and helped avoid leakage.

---

## Expected Outputs

- Demand trend visualizations
- Hourly and seasonal usage patterns
- Correlation analysis
- Model comparison using MAE, RMSE, and R²
- Feature importance analysis for the final tree-based model

---

## Key Learning Goals

- Apply time-aware validation correctly
- Build forecasting-style features with lag and rolling windows
- Compare baseline and ensemble regression models
- Interpret seasonal demand behavior in a business-friendly way

---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook

---

## Summary

This project extends my previous tabular machine learning work into a time series setting while keeping the workflow practical and interpretable.

It demonstrates:

- exploratory data analysis for temporal data
- feature engineering for forecasting
- regression model comparison
- time-aware validation and interpretation
