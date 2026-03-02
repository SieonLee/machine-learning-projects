# Australian Rental Market Fair Price Prediction & Underpriced Listing Detection

## Project Overview

This project aims to estimate the fair market rental price of residential properties across Australia using structured listing data.

Beyond simple price prediction, the project identifies potentially underpriced listings by comparing the actual listed rent with the model-estimated fair price.

The objective is not only predictive performance, but also to demonstrate practical data science considerations such as:

- Real estate price modeling with structured tabular data
- Feature engineering using amenities and local market signals
- Model comparison (linear vs tree-based vs boosting)
- Business-oriented scoring for deal detection
- Practical marketplace applications for pricing intelligence

## Problem Definition

**Task:** Regression + Ranking  
**Target Variable:** `price_display`

### Main Questions

- Can we estimate the fair market weekly rent of a property using location, structure, and amenity features?
- Can we identify listings that appear underpriced relative to similar properties in the market?

## Dataset

**Source:** `australian_rental_market_2026.csv`  
**Final size:** 6,767 listings  
**Modeling size after cleaning:** 6,758 listings

### Key Features
- `propertyType`
- `state`
- `suburb`
- `bedrooms`
- `bathrooms`
- `parking_spaces`
- `amenities`
- `price_display`

The dataset includes property structure, location, and amenity information, making it suitable for fair-price estimation and value scoring.

## Methodology

### 1. Data Preprocessing

- Removed unrealistic price outliers
- Removed structural anomalies such as extreme bedroom counts
- Filled missing amenity values
- Selected key predictors:
  - `bedrooms`
  - `bathrooms`
  - `parking_spaces`
  - `propertyType`
  - `state`
  - amenity-derived features
  - suburb-level pricing signal

### 2. Feature Engineering

To improve predictive performance, several additional features were created:

- `amenity_count`
- Binary amenity flags:
  - `has_aircon`
  - `has_balcony`
  - `has_dishwasher`
  - `has_pool`
  - `has_pets`
  - `has_gym`
- `suburb_median_price`

This feature engineering step was important because rental pricing depends not only on property size, but also on neighborhood context and quality-of-life amenities.

### 3. Model Training

The dataset was split into train and test sets, and three models were compared:

- **Ridge Regression** for a linear baseline
- **Random Forest** for non-linear interactions
- **XGBoost** for higher predictive performance

### 4. Underpriced Listing Detection

After predicting fair market prices, a **Value Score** was computed:

**Value Score = (Predicted Fair Price - Actual Price) / Predicted Fair Price × 100**

This score was used to classify listings into:

- Best Deal (>20% below market)
- Good Deal (10–20% below market)
- Fair Price
- Slightly Overpriced
- Overpriced (>20% above market)

## Models

| Model | Purpose |
|---|---|
| Ridge Regression | Baseline, simple and interpretable |
| Random Forest | Non-linear interactions and robust tabular modeling |
| XGBoost | Strong predictive performance and value ranking |

## Results

| Model | RMSE (AUD) | MAPE (%) | R² |
|---|---:|---:|---:|
| Ridge Regression | 190.8 | 13.98 | 0.6893 |
| Random Forest | 196.0 | 11.99 | 0.6720 |
| XGBoost | 193.6 | 11.91 | 0.6800 |

## Key Observations

- Ridge Regression achieved the best R², showing strong overall explanatory power.
- XGBoost achieved the lowest MAPE, making it the most useful model for practical pricing and deal detection.
- Location was the strongest pricing driver, especially through `suburb_median_price`.
- Bedrooms and bathrooms were among the most influential structural predictors.
- Amenity variables added meaningful incremental signal.

## Insights from EDA

- Rental prices are heavily right-skewed, with most listings concentrated in the mid-range and a smaller number of luxury properties forming a long tail.
- Average rents differ substantially across states, with NSW and ACT showing the highest pricing levels.
- Houses and townhouses generally command higher rents than studios, flats, and smaller unit types.
- Rental prices increase consistently with the number of bedrooms and bathrooms.
- Geographic variation plays a major role in explaining market price differences.

## Deal Detection Summary

- Best Deal listings: 303
- Good Deal listings: 926
- Total deal listings: 1,229
- Deal rate: 18.2% of all cleaned listings

This suggests that nearly one in five listings in the dataset may be priced below the model-estimated market value.

## Business Applications

- Rental platform “Best Value” recommendations
- Fair-price transparency for renters
- Deal alert systems for high-value listings
- Pricing intelligence dashboards for marketplaces
- Agency benchmarking based on listing value quality

## Limitations and Considerations

- `suburb_median_price` was calculated using the full dataset, which may introduce leakage in a strict production setting.
- The dataset represents listed prices, not necessarily final negotiated rental outcomes.
- Amenity information is text-derived and may be inconsistently reported across listings.
- Additional signals such as listing age, market trends, and text embeddings could further improve performance.

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- XGBoost
- matplotlib
- seaborn

## Summary

This project demonstrates:

- Fair market rent prediction using structured property data
- Practical feature engineering with local market and amenity signals
- Comparison of baseline and advanced machine learning models
- Underpriced listing detection through value scoring
- Business-oriented thinking for rental marketplace applications
