# 📌 Business Context

Many individuals lack traditional credit history and are excluded from formal financial systems. Home Credit aims to improve financial inclusion by leveraging alternative data sources (bureau data, previous applications, installment payments, etc.) to better assess repayment ability.

This project builds a predictive model to estimate the probability that a client will default on a loan.

---

# 🔄 Project Workflow (CRISP-DM)

## 1️⃣ Business Understanding

* Define loan default prediction problem
* Identify key success metric: AUC (Area Under ROC Curve)
* Emphasize fairness, risk control, and leakage prevention


## 2️⃣ Data Understanding (EDA)

Exploratory Data Analysis performed in:

```
EDA.Rmd
```

Key steps:

* Target distribution analysis
* Missing value assessment
* Feature distributions (numeric & categorical)
* Default rate by key variables
* Correlation analysis
* External source score evaluation
* Aggregated transactional data exploration

Supplementary datasets explored:

* Bureau
* Bureau Balance
* Previous Applications
* Installments Payments

Insights from EDA informed feature engineering decisions.



## 3️⃣ Data Preparation Pipeline

Implemented in:

```
data_preparation.Rmd
```

### ✅ Design Principles

* Reproducible
* Train/Test consistency
* No data leakage
* Reusable functions
* Fit/Transform architecture



### 🏗 Feature Engineering

* Aggregated bureau features (mean, max, min, counts)
* Credit duration features
* Loan history summaries
* Missing value imputation (training statistics only)
* Numeric scaling
* Categorical encoding

All aggregations were performed at `SK_ID_CURR` level before joining to application data.

---

### 🔁 Reusable Preprocessing Functions

```r
prep <- fit_prep(train_joined)
train_final <- transform_with_prep(train_joined, prep)
test_final  <- transform_with_prep(test_joined, prep)
```

**Key Guarantee:**

* All statistics (means, medians, bins) computed using training data only
* Identical feature columns in train and test
* TARGET excluded from test

This ensures full compliance with leakage prevention best practices.



## 4️⃣ Modeling

Implemented in:

```
modeling.Rmd
```

### Models Evaluated

* Logistic Regression
* Regularized models
* Tree-based models (if applicable)
* Cross-validation approach

### Evaluation Metrics

* ROC Curve
* AUC
* Confusion Matrix
* Feature Importance

Model comparison performed using consistent validation methodology.



# 📊 Repository Structure

```
home-credit-project/
│
├── EDA.Rmd
├── data_preparation.Rmd
├── modeling.Rmd
├── .gitignore
└── README.md
```

---

# 🧠 Key Technical Highlights

* CRISP-DM structured workflow
* Leakage-safe preprocessing pipeline
* Feature aggregation across relational datasets
* Fit/Transform design pattern
* Train/Test reproducibility
* Cross-validated modeling
* Clean modular R Markdown implementation


# 📈 Results

* Successfully engineered aggregated credit history features
* Built reproducible ML pipeline
* Achieved competitive AUC performance
* Demonstrated proper ML workflow from EDA to deployment-ready preprocessing



# 🛠 Technologies Used

* R
* tidyverse
* dplyr
* ggplot2
* caret / tidymodels (if used)
* CRISP-DM methodology



#  Academic Context

This project was completed as a **Capstone Project** as part of a graduate-level Business Analytics/Data Science program.

The focus was not only on predictive performance but also on:

* Reproducibility
* Statistical rigor
* Documentation quality
* Alignment with assignment rubric



# 🚀 Future Improvements

* Hyperparameter tuning
* Model stacking / ensemble learning
* SHAP value interpretation
* Deployment via API
* Fairness & bias evaluation


