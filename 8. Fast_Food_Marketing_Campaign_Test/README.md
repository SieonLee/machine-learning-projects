# Fast Food Marketing Campaign A/B/C Test Analysis

## Overview

This project evaluates the effectiveness of three marketing campaigns (Promotion 1, 2, and 3) using weekly store-level sales data.

The objective is to determine whether statistically significant differences exist among the campaigns and to provide a data-driven recommendation for large-scale rollout.

Statistical hypothesis testing, effect size analysis, and regression modeling were applied to quantify both statistical and practical impact.

---

## Business Problem

A fast food company launched three promotional strategies across multiple markets.

**Key Question:**
Which promotion generates the highest weekly sales, and should be scaled company-wide?

---

## Dataset

- 548 observations
- Store-level weekly sales data
- 4 weeks per store
- 3 promotion types (A/B/C equivalent)

### Key Variables

- `Promotion` – Campaign type (1, 2, 3)
- `SalesInThousands` – Weekly sales (target variable)
- `MarketSize` – Small, Medium, Large
- `AgeOfStore` – Store operating age
- `LocationID` – Store identifier

---

## Methodology

### 1. Exploratory Data Analysis (EDA)

- Verified balanced group distribution
- Compared mean and variance across promotions
- Assessed potential confounders (market size, store age)

---

### 2. One-Way ANOVA

Tested whether mean sales differ across promotion groups.

- F-statistic: 21.95
- p-value: < 0.001

Result: At least one promotion differs significantly.

---

### 3. Post-Hoc Analysis (Tukey HSD)

Identified pairwise differences:

- Promotion 1 vs 2 → Significant difference
- Promotion 2 vs 3 → Significant difference
- Promotion 1 vs 3 → Not significant

Promotion 2 underperforms relative to both 1 and 3.

---

### 4. Effect Size

Eta squared (η²) = 0.075

Interpretation:
Promotion type explains approximately 7.5% of the variance in weekly sales, indicating a moderate practical effect.

---

### 5. Regression Adjustment

Built an OLS regression model controlling for:

- Market Size
- Store Age

Key Findings:

- Promotion 2 generates ~$10.75k lower weekly sales than Promotion 1 (p < 0.001)
- Promotion 3 is not significantly different from Promotion 1
- Market size is the strongest predictor of sales performance
- Model R² = 0.582

---

## Key Insights

- Promotion 2 consistently underperforms.
- Promotion 1 and 3 show comparable performance.
- Market size has greater impact on sales than promotion type.
- Statistical significance aligns with regression-adjusted results.

---

## Business Recommendation

Promotion 2 should not be scaled further due to statistically and practically significant underperformance.

Promotions 1 and 3 deliver similar results. If implementation costs are equivalent, Promotion 1 may be preferred due to slightly higher average sales.

Future campaign strategies should incorporate market segmentation, as market size is a primary driver of revenue variability.

---

## Limitations

- Store-level aggregated data (no customer-level granularity)
- Repeated weekly measurements may introduce autocorrelation
- Campaign cost data unavailable (ROI not calculated)

---

## Future Improvements

- Mixed-effects modeling to account for repeated store observations
- ROI analysis incorporating campaign cost
- Heterogeneous treatment effect analysis by market size
- Customer-level A/B testing for stronger causal inference

---

## Tech Stack

- Python
- pandas
- scipy
- statsmodels
- seaborn
- matplotlib
