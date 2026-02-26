# home-credit-project

## Home Credit Default Risk Prediction — Machine Learning Capstone

A full end-to-end credit risk modeling project based on the Kaggle Home Credit Default Risk competition. The objective is to predict the probability of loan default using demographic, financial, and behavioral credit data.

This project follows a structured CRISP-DM workflow and emphasizes reproducibility, leakage prevention, feature engineering, and model performance optimization.

## Business Context

Many individuals lack sufficient credit history and are excluded from traditional lending systems. This project simulates how Home Credit Group can use alternative data (bureau records, transaction history, installment behavior, POS and credit card usage) to better assess repayment risk and improve financial inclusion.

##Project Workflow (CRISP-DM)
### 1️. Data Preparation Pipeline

A production-style preprocessing framework ensures:

  - Reusable fit/transform design

  - All preprocessing statistics (medians, bin thresholds, feature drops) learned from training data only

  - Identical transformations applied to test data

- Train/Test consistency

  - Same feature space enforced across datasets

  - Strict leakage prevention

- Robust data cleaning

  - Fixed anomalies (e.g., DAYS_EMPLOYED = 365243)

  - Missing value imputation using train-derived medians

  - Missing indicators where appropriate

- Feature engineering

  - Days → years transformations

  - Financial ratios and interaction terms

  - Binned demographic variables

  - Aggregated behavioral features

- Applicant-level aggregation

  - Supplementary tables aggregated to SK_ID_CURR:

  - bureau.csv

  - previous_application.csv

  - installments_payments.csv

  - POS_CASH_balance.csv

  - credit_card_balance.csv

## Predictive Modeling
### Task 1 — Baseline Benchmark

- Majority class baseline

- Logistic regression benchmark

- Evaluation using AUC (not accuracy due to class imbalance)

### Task 2 — Model Comparison

Compared multiple model types:

  - Logistic Regression

  - Random Forest

  - XGBoost (primary model)

Performance estimated using:

  - 3-fold cross-validation

  - Out-of-sample AUC

  - Stratified sampling

  - Efficient runtime strategies

### Task 3 — Class Imbalance Handling (~8% default rate)

Evaluated:

  - No adjustment

  - Downsampling

  - Upsampling

Compared CV AUC across approaches.

### Task 4 — Hyperparameter Tuning

Optimized XGBoost using:

  - Randomized search (not grid)

  - 5K subsample for tuning

  - 3-fold CV

  - Early stopping

  - Final model trained on full training dataset

### Task 5 — Supplementary Feature Impact

Evaluated incremental AUC improvement:

| Feature Set	        | CV AUC |
| ------------------- | ------ |
| Application only	  | ~0.71  |
|+ Bureau / Previous / Installments	| ~0.72 |
| + POS / Credit Card	| ~0.73 |

Demonstrated measurable performance gains from behavioral credit data.

### Task 6 — Kaggle Submission

- Generated predicted probabilities for test set

- Enforced strict feature alignment

- Corrected submission formatting issues (integer ID handling)

- Produced Kaggle-ready submission file

(Note: Competition is closed; performance evaluated using cross-validated AUC.)

## Performance Optimization Strategies

To ensure computational efficiency:

- 3-fold cross-validation

- Subsampled tuning (5K–15K rows)

- Randomized search (~5–10 iterations)

- Direct XGBoost API (avoiding heavy wrappers)

- Warning suppression and stable aggregation functions

- Stratified sampling to prevent empty-fold AUC errors

## Technologies Used

- R
- dplyr
- xgboost
- readr
- CRISP-DM framework
- Kaggle competition dataset

### Key Takeaways

- Behavioral credit history significantly improves default prediction.

- Proper feature engineering contributes incremental but meaningful AUC gains.

- Handling class imbalance and preventing data leakage are critical in credit modeling.

- Reproducible preprocessing pipelines are essential for production-ready ML systems.

### Project Status

- Complete end-to-end modeling pipeline
- Hyperparameter-tuned XGBoost model
- Kaggle submission generated
- Production-style preprocessing design
