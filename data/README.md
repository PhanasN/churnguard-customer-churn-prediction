# Data

The original account-level customer dataset used in this analysis is not included in this repository, because it is proprietary business data.

## Schema

The dataset contained 11,260 unique customer accounts with 19 fields covering 12 months of activity, including:

- Account tenure (months)
- Customer segment (e.g. Regular, Regular Plus)
- Number of users on the account
- Complaint history (whether a complaint was logged)
- Customer support / agent interaction score
- Marital status / account holder profile
- Usage and spend metrics
- Churn label (churned / retained)

## Reproducing this analysis

To reproduce the analysis with your own data:

1. Prepare a customer-account-level dataset with a binary churn label and the feature categories listed above.
2. Place the file in this `data/` folder (this folder is excluded from version control by default; see `.gitignore`).
3. Update the file path referenced in `src/data_cleaning.py`.
4. Run the notebook or scripts in order: data cleaning, exploratory analysis, model training, model evaluation, risk tiering.

## Synthetic data option

If you do not have an equivalent dataset, a synthetic dataset generator can be added to approximate the structure above for demonstration purposes. This is not included by default to avoid implying the results would match the original findings.
