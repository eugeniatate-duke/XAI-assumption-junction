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
| Linear regression | Linearity, homoscedasticity, normal residuals, independence | Residuals-versus-fitted plot, residual histogram, Q-Q plot, Breusch-Pagan test, Shapiro-Wilk test, and dataset-structure review | The residuals are not normally distributed and residual variance is not constant. Churn is binary, so linear regression is only a baseline |
| Logistic regression | Binary outcome, independence, no perfect separation, linearity in the log-odds, limited multicollinearity, sufficient sample size | Binary target check, category churn-rate summary, separation check, binned log-odds plots, correlation heatmap, and events-per-predictor calculation | Some numeric relationships are nonlinear, and `tenure` is strongly correlated with `TotalCharges` |
| GAM | Appropriate binary outcome and logistic link, independence, nonlinear effects, additive structure | `LogisticGAM`, binned churn-rate plots, and GAM partial-dependence plots | The additive model does not include interactions, and the `TotalCharges` effect is irregular and should be interpreted cautiously |

## Model Comparison

| Model | Performance Evidence | Interpretability Strength | Interpretability Weakness |
|---|---|---|---|
| Linear regression | R² = 0.2616, RMSE = 0.3794, MAE = 0.3004, ROC-AUC = 0.8297 | Coefficients are straightforward to inspect and interpret as changes in a continuous score | Not designed for a binary target and produced a negative prediction, which is not a valid churn probability |
| Logistic regression | ROC-AUC = 0.8423, accuracy = 0.8027, precision = 0.6529, recall = 0.5481, F1 = 0.5959 | Appropriate for binary churn prediction; coefficients can be interpreted as odds ratios | Assumes linear relationships between predictors and the log-odds of churn; correlated predictors can make individual coefficients difficult to interpret |
| GAM | ROC-AUC = 0.8476, accuracy = 0.8062, precision = 0.6667, recall = 0.5401, F1 = 0.5968 | Captures nonlinear effects while allowing individual feature contributions to be visualized | Smooth curves are more complex to interpret than logistic odds ratios, and some effects may be unstable or difficult to explain |

## Recommendation

Recommended model: Logistic regression as the primary operational model, with the GAM as a supporting analysis tool.

Why this model: Logistic regression provides valid churn probabilities, strong performance, and
straightforward coefficient interpretation through odds ratios. The GAM achieved a
slightly higher ROC-AUC and F1 score and is useful for examining nonlinear effects, but
the performance improvement over logistic regression was modest.

What the company can responsibly conclude:

- Some customer groups have different observed churn rates.
- Contract type, internet service, technical support, online security, payment method, and tenure are associated with predicted churn risk.
- The models can help prioritize customers for possible retention outreach.
- The GAM provides evidence that some feature relationships, especially tenure, are nonlinear.


What the company should not conclude yet:

- The models do not prove that any feature causes churn.
- A high predicted churn probability does not guarantee that a customer will leave.
- The results should not automatically be generalized to future customers or other telecommunications companies without additional validation.
- The model should not be deployed without considering the costs of false positives and missed churners.

One next analysis we would run:

Evaluate different probability thresholds and compare the business cost of missed churners
with the cost of unnecessary retention outreach. Model performance should also be checked
across important customer subgroups before deployment.
