# Monsoon Credit Tech - Credit Risk Prediction Assignment

## Overview

This project aims to predict the probability of default for borrowers using credit bureau account history and enquiry data. The solution involves transforming nested JSON bureau records, performing feature engineering, and training machine learning models to generate risk scores for unseen borrowers.

---

## Dataset

The assignment consists of:

- `train_flag.csv`
- `test_flag.csv`
- `accounts_data_train.json`
- `accounts_data_test.json`
- `enquiry_data_train.json`
- `enquiry_data_test.json`

The account and enquiry datasets contain nested JSON records that were transformed into a structured long format before feature engineering.

---

## Approach

### 1. Data Transformation
- Converted nested account records into a loan-level dataset.
- Converted nested enquiry records into an enquiry-level dataset.
- Parsed payment history strings to extract delinquency (DPD) information.

### 2. Feature Engineering

Created borrower-level features from:

#### Account Features
- Number of loans
- Active vs closed loans
- Loan amount statistics
- Credit type diversity
- Overdue statistics

#### Payment History Features
- Maximum DPD
- Average DPD
- Delinquency counts
- 30/60/90+ DPD indicators

#### Enquiry Features
- Number of enquiries
- Enquiry amount statistics
- Enquiry recency features
- Enquiry velocity features

#### Derived Features
- Active exposure
- Loan concentration
- Active-to-closed loan ratio
- Enquiries per loan
- Credit mix ratios

---

## Modeling

Two models were evaluated using 5-Fold Stratified Cross Validation with ROC-AUC as the evaluation metric:

| Model | CV ROC-AUC |
|---------|---------|
| LightGBM | 0.6558 |
| CatBoost | 0.6745 |

CatBoost achieved the best performance and was selected as the final model.

---

## Key Findings

- Enquiry recency was the strongest predictor of borrower risk.
- Active credit exposure and loan tenure features contributed significantly.
- Credit-seeking behavior showed stronger predictive power than repayment history features.

---

## Output

The final submission file contains: uid,TARGET