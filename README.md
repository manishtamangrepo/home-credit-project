# home-credit-project
Home Credit Default Risk Prediction — A machine learning capstone project analyzing consumer credit data to predict loan default risk using feature engineering, EDA, and predictive modeling.
Many individuals struggle to obtain loans due to insufficient or non-existent credit histories. Unfortunately, this underserved population is often exposed to unfair or unreliable lending practices.

Home Credit Group aims to improve financial inclusion by providing safe, transparent, and responsible lending to the unbanked population. To achieve this, Home Credit leverages a wide range of alternative data sources, including telecommunications and transactional data, to better assess clients’ repayment abilities.

This project is based on the Home Credit Default Risk competition from Kaggle and serves as my school capstone project.

## Data Preparation Pipeline (CRISP-DM)

This repository contains a production-ready data preparation pipeline developed as part of a CRISP-DM–based analytics workflow. The focus is on reproducibility, train/test consistency, and leakage prevention, translating exploratory data analysis (EDA) findings into reusable code suitable for modeling.

## Key Features
  - Reusable fit/transform design
  - All preprocessing parameters (medians, bin thresholds, column drops) are learned from training data only and reused for test data.

## Train/Test consistency enforced
  - Identical transformations and feature columns are produced for train and test datasets (except TARGET).

## Robust data cleaning

  - Fixes known anomalies (e.g., DAYS_EMPLOYED = 365243)

  - Handles missing values with indicators and train-derived imputations

## Feature engineering

  - Demographic transformations (days → years)

  - Financial ratios, interaction terms, and binned variables

## Applicant-level aggregation
  - Supplementary datasets (bureau, previous applications, installment payments) are aggregated to SK_ID_CURR and joined to the application data.

## Production-ready behavior
  - Functions execute silently and return clean data objects, consistent with real-world pipelines.

## Structure

  - Task 1–2: Cleaning and feature engineering from application data

  - Task 3–4: Aggregation and joining of supplementary data

  - Task 5: Explicit enforcement of train/test consistency

This pipeline is designed to be modular, extensible, and model-agnostic, serving as a reliable foundation for downstream modeling.
