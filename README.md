# Credit-Risk Modelling with Default of Credit Card Clients

---

## 1. Project Information

- **Project Title:** Credit Risk Prediction using Machine Learning  

- **Group Members:**  
  - Tanguy CONVERSET  

- **Course Name:** AI In Finance  
- **Instructor:** Nicolas De Roux & Mohamed EL FAKIR  
- **Submission Date:** April 21, 2026  

---

## 2. Project Description

This project focuses on **credit risk modeling**, aiming to predict whether a credit card client will default on their payment.

Financial institutions rely heavily on such models to assess customer risk before granting credit. Poor risk estimation can lead to significant financial losses, while accurate predictions improve profitability and decision-making.

This project is particularly relevant for:
- Banks and financial institutions  
- Credit scoring systems  
- Fintech companies  

---

## 3. Project Goal

The goal of this project is to **predict whether a client will default on their next payment** using financial and behavioral data.

A successful model should:
- Accurately identify high-risk clients  
- Support credit decision-making  
- Provide reliable risk scores  

---

## 4. Task Definition

- **Task Type:** Binary Classification  

- **Input Variables:**  
  Financial, demographic, and behavioral variables such as:
  - Credit limit  
  - Payment history  
  - Billing amounts  
  - Repayment amounts  
  - Engineered features (credit usage, payment ratio, etc.)  

- **Target Variable:**  
  `default.payment.next.month`  

- **Evaluation Metrics:**  
  - ROC-AUC  
  - F1-score  
  - Accuracy  

---

## 5. Dataset Description

### Dataset Overview

- **Number of samples:** 30,000  
- **Number of features:** 27  
- **Target variable:** default.payment.next.month  
- **Source:** UCI Credit Card Default Dataset  

---

### Feature Description

| Feature | Description | Type |
|--------|------------|------|
| LIMIT_BAL | Credit limit | Numerical |
| SEX | Gender | Categorical |
| EDUCATION | Education level (cleaned) | Categorical |
| MARRIAGE | Marital status (cleaned) | Categorical |
| AGE | Age | Numerical |
| PAY_0 to PAY_6 | Repayment status history | Ordinal |
| BILL_AMT1 to BILL_AMT6 | Billing amounts | Numerical |
| PAY_AMT1 to PAY_AMT6 | Payment amounts | Numerical |
| utilisation_credit_moy | Average credit usage | Numerical |
| utilisation_credit_max | Max credit usage | Numerical |
| ratio_paiement | Payment ratio | Numerical |
| age_group | Age group | Categorical |

---

### Target Variable

- **Name:** `default.payment.next.month`  
- **Meaning:** Whether a client defaults next month  
- **Values:**  
  - 0 → No default  
  - 1 → Default  

---

### Data Types

- Numerical variables (financial amounts, age)  
- Categorical variables (gender, education, marriage)  
- Ordinal variables (repayment history)  
- Engineered features  

---

### Data Distribution

- Imbalanced dataset (fewer defaults)  
- Skewed financial variables  
- Presence of extreme values  

---

### Data Quality

- Removed **ID column**  
- Cleaned **EDUCATION** and **MARRIAGE**  
- No significant missing values  
- Class imbalance present  

---

## 6. Data Preprocessing

- Removed **ID column** (non-informative)  
- Cleaned categorical variables  
- Feature engineering:
  - `utilisation_credit_moy`
  - `utilisation_credit_max`
  - `ratio_paiement`
  - `age_group`
- No scaling or encoding applied (tree-based models used)  

---

## 7. Modeling Approach

### Models Used

- Logistic Regression  
- Random Forest  
- XGBoost  
- MLP (Neural Network)  

---

### Modeling Strategy

- Train/test split  
- Logistic Regression as baseline  
- Cross-validation on Random Forest  

Cross-validation scores:
[0.8639, 0.8625, 0.8654, 0.8854, 0.8846]


- Overfitting analysis:
  - Train AUC: 0.9218  
  - Test AUC: 0.8786  

- Probability calibration applied  

---

### Evaluation Metrics

- **ROC-AUC** → best for imbalanced classification  
- **F1-score** → balance between precision and recall  
- **Accuracy** → overall performance  

---

### Model Performance

#### Logistic Regression
- AUC: 0.7283  
- F1: 0.6656  

#### Random Forest
- AUC: 0.8786  
- F1: 0.7904  

#### XGBoost
- AUC: 0.8445  
- F1: 0.7485  

#### MLP
- AUC: 0.8458  
- F1: 0.7804  

---

### Best Model

**Random Forest** achieved the best performance.

---

### Calibration

- Calibrated AUC: **0.9758**

---

## 8. Model Interpretability

### SHAP Insights

- **PAY_0** is the most important feature  
- Payment history (PAY_X) is the strongest predictor  
- High credit usage increases risk  
- Low repayments increase default probability  

---

### Feature Importance (Top 10)

| Feature | Importance |
|--------|----------|
| PAY_0 | 0.187 |
| PAY_2 | 0.084 |
| utilisation_credit_max | 0.049 |
| PAY_3 | 0.049 |
| utilisation_credit_moy | 0.048 |
| PAY_4 | 0.044 |
| PAY_AMT1 | 0.042 |
| PAY_5 | 0.038 |
| PAY_AMT2 | 0.037 |
| BILL_AMT1 | 0.037 |

---

### Key Insight

> Past repayment behavior is the strongest predictor of future default.

---

## 9. Project Structure
project/
│
├── notebook.ipynb
├── data/
├── README.md
└── requirements.txt


---

## 10. Installation

Install dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap kagglehub
