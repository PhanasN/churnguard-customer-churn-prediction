# ChurnGuard: Customer Churn Prediction & Retention Intelligence

ChurnGuard is an end-to-end customer retention analytics project built on 11,260 account-level records. It combines exploratory data analysis and predictive modelling into one reproducible pipeline, moving from a business question to a deployable risk-scoring system.

## The business question

Where is churn risk concentrated, and what intervention can the business defend financially?

The project does not start with a model. It starts by understanding where churn actually concentrates, then tests whether that understanding can be converted into a reliable, auditable prediction system.

## Project structure

The analysis is organized in two connected stages:

1. **Business insights and diagnosis** – data quality validation, churn distribution analysis, and driver identification.
2. **Predictive modelling** – model comparison, tuning, validation, and conversion of model output into an operational retention workflow.

## Key findings: diagnosis stage

- 16.8% of accounts had churned; 83.2% were retained.
- Accounts in their first three months churned at 42.3%, versus approximately 0% beyond 24 months.
- Accounts with a logged complaint churned at 31.8%, versus 11.1% without one.
- The Regular Plus segment had the highest segment-level churn rate at 27.1%.
- Tenure and complaint history were the strongest individual risk signals identified through correlation analysis.

## Model results: prediction stage

Seven classification approaches were compared under consistent conditions using F1 score for the churn class, because with only 16.8% of accounts churning, a model predicting "no churn" for everyone would appear roughly 83% accurate while catching zero real churners.

| Model | Cross-validated F1 (churn class) |
|---|---|
| XGBoost | 0.88 |
| Random Forest | 0.86 |
| KNN | 0.86 |
| SVM (RBF kernel) | 0.81 |
| Decision Tree | 0.75 |
| Logistic Regression | 0.58 |
| Naive Bayes | 0.43 |

The final tuned **XGBoost** model was evaluated on a held-out test set of 2,252 accounts not used in training or tuning:

- **89-90% recall** – correctly identified the large majority of accounts that later churned.
- **95-97% precision** – the large majority of flagged accounts were genuine churn risks.
- **ROC-AUC of 0.99** for overall risk ranking.
- Low false-alarm rate among retained accounts.

The model independently confirmed tenure and complaint history as the dominant churn drivers, and surfaced a new hypothesis (higher churn among multi-user accounts) flagged for business validation rather than immediate action.

## From score to action

Model output is converted into risk tiers (Low / Medium / High) to produce a focused, auditable priority list for the retention team, rather than a blanket campaign across an entire customer segment. The recommended operating logic:

1. Score accounts regularly or immediately after a complaint is logged.
2. Prioritize the High-risk tier.
3. Lead with service-based outreach and problem resolution.
4. Reserve discounting for confirmed high-value accounts.
5. Test the intervention against a matched control group before scaling.

## Limitations and responsible interpretation

- The model is validated on held-out historical data, not yet tested in a live retention workflow.
- High predictive performance does not prove that contacting a flagged account prevents churn; this requires a controlled test against a matched group.
- The relationship between account user count and churn needs further business validation before being used as a targeting rule.
- Model performance should be monitored on an ongoing basis, since customer behavior and operating conditions can change.

## Repository structure

```
churnguard-customer-churn-prediction/
├── README.md
├── Customer_Churn_Final_Report.ipynb
├── ChurnGuard_Final_Report_Phanas.pdf
├── figures/
│   ├── data_quality/
│   ├── exploratory_analysis/
│   ├── model_comparison/
│   ├── model_validation/
│   └── risk_tiering/
├── src/
│   ├── data_cleaning.py
│   ├── feature_engineering.py
│   ├── exploratory_analysis.py
│   ├── model_training.py
│   ├── model_evaluation.py
│   └── risk_tiering.py
├── requirements.txt
└── data/
    └── README.md
```

## Data

The original account-level dataset is not included in this repository. See `data/README.md` for a description of the schema and instructions for reproducing the analysis with your own data or a synthetic sample.

## Skills demonstrated

Data Quality Management, Exploratory Data Analysis, Feature Engineering, Predictive Modelling, Classification (XGBoost, Random Forest, KNN, SVM, Decision Tree, Logistic Regression, Naive Bayes), Imbalanced Classification (SMOTE), Cross-Validation, Precision/Recall/F1, ROC-AUC, Risk Scoring, Retention Strategy, Python, Pandas, Scikit-learn.

## Status

Both stages are complete: business diagnosis and predictive model validation. The next phase is a live controlled test of the retention intervention against a matched control group.
