# Shinkansen Passenger Experience Prediction — Hackathon Report

**Competition Dates:** Oct 1, 11:00 PM – Oct 5, 11:00 PM
**Placement:** 4th out of 37 teams
**My Final Score:** 95.84855% Accuracy
**Winning (1st place) Score:** 95.96090%

---

## Problem Overview

The challenge was based on the Shinkansen Bullet Train in Japan, focusing on passengers’ travel satisfaction. The task was to build a machine learning model to predict whether a passenger was satisfied (1) or not satisfied (0) with their overall experience.

Two datasets were provided:

* **Traveldata_train.csv** — passenger information and trip attributes.
* **Surveydata_train.csv** — survey feedback, including satisfaction labels.

The goal was to predict passenger satisfaction on unseen test data.

---

## Objective

The objective was to identify which features most influence passengers’ overall experience and to develop a predictive model with high generalization performance.

**Target Variable:**

* `Overall_Experience`

  * `1` → Satisfied
  * `0` → Not Satisfied

**Evaluation Metric:**

* Accuracy: the proportion of correct predictions over total observations.

---

## Approach

I chose to work individually instead of forming a team. My approach focused entirely on **CatBoost**, which proved to be extremely effective and simple to use.

### Why CatBoost?

* Natively handles categorical features; no need for encoding.
* Automatically manages missing values; no need for manual imputation.
* Robust to outliers.
* Minimal preprocessing required while maintaining strong accuracy.

CatBoost consistently delivered the best results on both training and unseen test data compared to other models I tried, including LightGBM and XGBoost.

---

## Final Model Configuration

The CatBoost model that produced the best results had the following parameters:

* `iterations=3000`: Sufficient boosting rounds to learn complex patterns.
* `learning_rate=0.006`: Low rate improved convergence stability and generalization.
* `depth=12`: Deep trees captured complex feature interactions.
* `l2_leaf_reg=5`: Regularization prevented overfitting while retaining model complexity.
* `random_strength=1.8`: Added randomness to splits for robustness.
* `border_count=254`: High granularity improved continuous feature handling.
* `loss_function='Logloss'` and `eval_metric='Accuracy'`: Directly aligned with the classification objective.
* `od_type='Iter'` + `od_wait=300`: Early stopping prevented overfitting and wasted computation.
* `verbose=100`: Monitored training progress effectively.

---

## Dataset Summary

The datasets included:

* Passenger demographics and travel history
* Train performance metrics and delay information
* Survey feedback on multiple service parameters
* Overall experience labels as the target variable

Both training and test datasets were collected simultaneously from the same population, ensuring consistency.

---

## Results

| Metric                      | Value               |
| --------------------------- | ------------------- |
| Accuracy on training data   | 95.979%             |
| Accuracy on test submission | 95.84855%           |
| Leaderboard placement       | 4th out of 37 teams |

---

## Reflections

* CatBoost required minimal preprocessing while achieving high accuracy.
* Careful hyperparameter tuning, particularly `depth`, `l2_leaf_reg`, and `learning_rate`, helped balance learning and overfitting.
* Working individually allowed full control over feature handling and model selection.
* My score was within 0.11% of the top submission, demonstrating the model’s strong generalization.

---

## Future Improvements

* Explore CatBoost ensembles or stacking with complementary models.
* Perform threshold optimization to refine classification cutoffs.
* Analyze feature importance to better interpret drivers of satisfaction.
