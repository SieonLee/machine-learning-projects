# Fast Food Marketing Campaign A/B/C Test Analysis

## Overview

This project compares three fast food marketing campaigns using weekly store-level sales data.

What makes it useful is that it stays close to the kind of question a business team would actually ask: which promotion should we keep investing in, and is the difference large enough to matter beyond statistical significance alone?

---

## Problem Definition

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

Regression summary:

- Promotion 2 generates ~$10.75k lower weekly sales than Promotion 1 (p < 0.001)
- Promotion 3 is not significantly different from Promotion 1
- Market size is the strongest predictor of sales performance
- Model R² = 0.582

---

## Conclusion

The results point to a fairly clear business decision. Promotion 2 underperforms in both the ANOVA and the regression-adjusted analysis, so it is difficult to justify rolling it out further. Promotion 1 and Promotion 3 perform similarly, which means the practical choice between them would likely depend on execution cost, operational simplicity, or other business constraints not included in the dataset.

One of the more useful findings is that market size explains a substantial share of weekly sales variation. That matters because it suggests the company should not evaluate campaign performance in isolation. A promotion may look strong or weak partly because of where it was deployed, so segmentation should be part of any next-round testing strategy.

Taken together, the analysis supports a simple conclusion: stop investing in Promotion 2, treat Promotion 1 and 3 as the real contenders, and evaluate future campaign rollouts with market context in mind.

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
