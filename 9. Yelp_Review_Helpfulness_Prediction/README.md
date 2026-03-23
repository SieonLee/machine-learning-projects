# Yelp Review Helpfulness Prediction & Ranking

## Overview

This project looks at a product-facing question: which Yelp reviews are likely to be genuinely helpful, and can a model do enough to rank better reviews closer to the top?

I like this problem because it sits between NLP and product analytics. The point is not only to classify review helpfulness, but to build a scoring system that feels closer to how a real review platform would decide what deserves visibility.

---

## Problem Definition

**Task:** Classification + Ranking  
**Target Variable:** `helpful_label`

### Main Questions

- Can we predict whether a review will receive at least one helpful vote?
- Which text and behavioral signals are most associated with review helpfulness?
- Can predicted helpfulness scores be used to rank reviews more effectively within businesses?

---

## Dataset

This project uses the Yelp Academic Dataset, with the following files:

- `yelp_academic_dataset_review.json`
- `yelp_academic_dataset_user.json`
- `yelp_academic_dataset_business.json`
- `yelp_academic_dataset_tip.json`
- `yelp_academic_dataset_checkin.json`

Main variables used in this project include:

- review text
- useful vote count
- star rating
- review date
- user review history
- user helpfulness history
- business review count
- business average rating

The target is derived as:

- `helpful_label = 1` if `useful >= 1`
- `helpful_label = 0` otherwise

This framing turns review helpfulness into a practical binary prediction problem while also supporting ranking applications based on predicted helpfulness probability.

---

## Methodology

### 1. Data Preparation

- Load a manageable sample of Yelp reviews
- Parse review timestamps
- Join user-level and business-level metadata
- Remove rows with missing critical fields

### 2. Feature Engineering

Text and behavioral features include:

- review length
- word count
- exclamation count
- question mark count
- uppercase ratio
- average word length
- user review count
- user historical useful votes
- business review count
- business average stars

### 3. Modeling

The workflow compares:

- Logistic Regression baseline
- Random Forest Classifier
- Gradient Boosting Classifier

Predicted probabilities are then used as ranking scores.

### 4. Evaluation

Classification performance is evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC AUC

Ranking quality is evaluated using:

- Precision@k
- Mean helpful rate in top-ranked reviews

---

## Results

The final model comparison showed that behavioral and text-derived features can meaningfully predict review helpfulness.

### Classification Performance

- Logistic Regression
  - Accuracy: 0.7345
  - Precision: 0.8037
  - Recall: 0.5789
  - F1 Score: 0.6731
  - ROC AUC: 0.7966

- Random Forest Classifier
  - Accuracy: 0.7457
  - Precision: 0.7868
  - Recall: 0.6328
  - F1 Score: 0.7015
  - ROC AUC: 0.8203

- Gradient Boosting Classifier
  - Accuracy: 0.7490
  - Precision: 0.7937
  - Recall: 0.6327
  - F1 Score: 0.7041
  - ROC AUC: 0.8230

### Ranking Performance

- Mean Precision@5: 0.5323

## Conclusion

The overall pattern is consistent across both prediction and ranking: review helpfulness is not random, and it can be modeled reasonably well using a mix of text-derived and behavioral features. Gradient Boosting performed best on the classification task, which suggests the relationship between helpfulness and review characteristics is nonlinear and benefits from a more flexible model than plain logistic regression.

The ranking results are just as important as the raw classification scores. In practice, a review platform does not simply need to label reviews as helpful or not. It needs to surface better reviews near the top. The model's top-ranked outputs tended to contain reviews that were actually useful, which makes the project feel much closer to a real product decision problem than a standard classroom classification exercise.

What I like most about this project is that the features remain interpretable. Review length, reviewer history, business context, and writing style all contribute signal, which means the model is not just performing well numerically. It is also capturing patterns that make intuitive sense for a review platform trying to prioritize quality content.

---

## Product Implications

This project can support:

- surfacing more useful reviews at the top of business pages
- prioritizing high-quality user-generated content
- identifying reviews that may deserve more visibility
- improving search and recommendation quality in review platforms

---

## Tech Stack

- Python
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook
