# Yelp Review Helpfulness Prediction & Ranking

## Overview

This project focuses on predicting which Yelp reviews are likely to be helpful and building a simple ranking framework to surface the most useful reviews to users.

The objective is to combine text-derived signals, reviewer behavior, and business-level context into a practical machine learning workflow that supports review ranking and content prioritization.

This project focuses on:

- NLP-style text feature engineering
- reviewer and business behavioral feature engineering
- binary helpfulness prediction
- ranking reviews using predicted helpfulness probability
- offline evaluation with classification and ranking metrics

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

### Key Findings

- Gradient Boosting achieved the best overall performance across Accuracy, F1 Score, and ROC AUC.
- Random Forest also performed strongly, indicating that nonlinear behavioral and text-derived signals were useful.
- Logistic Regression provided a solid baseline but underperformed the tree-based ensemble models.
- The ranking output successfully surfaced reviews with high useful-vote counts near the top of the scored list.
- The NLP analysis showed that review text can be used not only for prediction, but also for qualitative insight into positive and negative restaurant experiences.

---

## Expected Outputs

- helpful vs non-helpful review distribution
- review length and usefulness relationship
- model comparison table
- feature importance analysis
- top-ranked review inspection

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

---

## Summary

This project extends my portfolio into NLP-adjacent ranking and content quality prediction using a large-scale review platform dataset.

It demonstrates:

- practical feature engineering from raw review text
- combining behavioral and content signals
- binary classification for product-style decision making
- ranking-oriented evaluation for real-world usefulness
- restaurant review analysis with positive and negative review examples
