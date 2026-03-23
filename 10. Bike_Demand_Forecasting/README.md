# Bike Demand Forecasting

## Overview

This project forecasts bike rental demand using time and weather information, with most of the value coming from treating the problem as a temporal system rather than a generic regression task.

That changes the workflow in important ways. Demand depends on recent history, recurring hourly behavior, and seasonal context, so the notebook focuses as much on time-aware feature design and evaluation as it does on the final model choice.

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

## Conclusion

The forecasting results suggest that bike demand is shaped by strong nonlinear patterns that a simple linear model cannot fully capture. Once lagged demand, rolling averages, weather, and calendar signals were added, the tree-based models pulled noticeably ahead of the baseline. Gradient Boosting delivered the strongest overall fit, while Random Forest remained competitive and slightly stronger on MAE.

The important lesson here is not just that one model scored better than another. It is that forecasting quality improved when the feature set respected how demand actually behaves over time. Short-term momentum, recurring hourly patterns, and seasonal context all mattered, and the time-aware validation setup gave a more realistic estimate of what would happen in deployment.

So the final conclusion is pretty practical: if the goal is to forecast near-term bike demand well enough to support staffing, inventory, or bike rebalancing decisions, then a tree-based forecasting workflow with lag and rolling features is much more appropriate than a simple linear baseline.

---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook
