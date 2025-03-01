# Fraud Detection in Metaverse Transactions using SAS

## Overview
This project focuses on detecting fraudulent transactions within a **Metaverse-based financial system** using **Logistic Regression and Decision Trees in SAS**. The model predicts whether a transaction is **legitimate (`0`) or fraudulent (`1`)** based on attributes such as **transaction amount, risk score, session duration, and login frequency**.

## Problem Statement
Fraudulent transactions pose a significant security and financial risk. This project aims to classify transactions into:
- **0 = Low-risk transactions (Legitimate)**
- **1 = High-risk transactions (Fraudulent)**

The challenge is to balance fraud detection accuracy while minimizing false positives.

## Dataset
- **Features Used:**
  - `amount`: Transaction value.
  - `risk_score`: Predicted risk score for a transaction.
  - `session_duration`: User session length.
  - `login_frequency`: Number of logins in the last 7 days.
  - `location_region`, `purchase_pattern`, `age_group`: Categorical user metadata.
- **Target Variable (`fraud_flag`)**: 
  - `0` → Low-risk transactions (Legitimate)
  - `1` → High-risk transactions (Fraudulent)

## Approach
1. **Data Preprocessing**
   - Convert original fraud labels into a **binary classification problem**.
   - Split dataset into **70% training, 30% testing**.

2. **Modeling in SAS**
   - **Logistic Regression (`PROC LOGISTIC`)**: Establishes a baseline fraud detection model.
   - **Decision Tree (`PROC HPSPLIT`)**: Captures complex non-linear fraud patterns.

3. **Evaluation Metrics**
   - **AUC-ROC Score**: `0.90`
   - **Precision**: `89%`
   - **Recall**: `89%`
   - **F1-Score**: `89%`

## Key SAS Code Snippets
### Logistic Regression in SAS
```sas
PROC LOGISTIC DATA=metaverse_train DESCENDING;
    CLASS fraud_flag (REF='0') location_region purchase_pattern age_group / PARAM=REF;
    MODEL fraud_flag = amount risk_score session_duration login_frequency / OUTROC=ROC_Logistic_AUC;
    OUTPUT OUT=Logistic_Predictions P=Pred_Prob;
RUN;
