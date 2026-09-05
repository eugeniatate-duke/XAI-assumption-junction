# Telco Customer Churn Interpretability

## Dataset

This project uses the Telco Customer Churn dataset from Kaggle: https://www.kaggle.com/datasets/blastchar/telco-customer-churn/data.
Each row represents a telecommunications customer and includes demographic, service, account, and billing information.

The goal is to understand which customer characteristics are associated with churn
and compare interpretable models for predicting whether a customer will leave the
company.

The target variable is `Churn`, encoded as:

- `0`: Customer stayed
- `1`: Customer churned

The dataset contains 7,043 customers. Approximately 26.5% of customers churned.

### Feature Groups

Demographic:

`gender`, `SeniorCitizen`, `Partner`, `Dependents`

Service:

`PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`,
`OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`,
`StreamingMovies`

Account:

`tenure`, `Contract`, `PaperlessBilling`, `PaymentMethod`

Billing:

`MonthlyCharges`, `TotalCharges`

## Assumption Checks

| Model | Key Assumptions Checked | Evidence | Concern |
|---|---|---|---|
| Linear regression | TBD | TBD | TBD |
| Logistic regression | TBD | TBD | TBD |
| GAM | TBD | TBD | TBD |

## Model Comparison

| Model | Performance Evidence | Interpretability Strength | Interpretability Weakness |
|---|---|---|---|
| Linear regression | TBD | TBD | TBD |
| Logistic regression | TBD | TBD | TBD |
| GAM | TBD | TBD | TBD |

## Recommendation

Recommended model: TBD

Why this model: To be completed after evaluating predictive performance, assumptions, and interpretability.

What the company can responsibly conclude:

- Some customer groups have different observed churn rates.


What the company should not conclude yet:

TBD

One next analysis we would run:

TBD
