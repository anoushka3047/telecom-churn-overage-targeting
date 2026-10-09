# Recovering Revenue from Overage-Paying, At-Risk Customers

A churn risk targeting analysis for a telecom provider.

## Problem
Customers who pay overage charges are valuable, but many of them are also likely to leave. The goal is to predict which customers are at high risk of churning and to find the group that is both at risk **and** paying overage today, so retention offers can be aimed where they protect the most revenue.

## Dataset
- About **100,000 customers**, split across a client table (`Client.csv`) and a usage record table (`Record.csv`).
- 57.1% of customers pay overage, averaging **$23.67/month** among payers.
- The data was provided through the course materials and is **not included** in this repository.

## Approach
1. **Exploratory analysis:** overage behaviour and churn rate by overage tier.
2. **Feature engineering:** `overage_ratio`, `has_overage`, `usage_intensity`, `drop_rate` and `chronic_overage`.
3. **Modelling:** three classifiers compared on a 20,000-customer test set.
4. **Business sizing:** estimate the revenue at stake in the high-risk, overage-paying segment.

## Results

| Model | ROC-AUC | Churn Recall | Churn Precision |
|---|---|---|---|
| Logistic Regression | 0.630 | 0.59 | 0.59 |
| Random Forest | 0.667 | 0.66 | 0.60 |
| Gradient Boosting | 0.682 | 0.65 | 0.62 |

**Model choice:** Random Forest was chosen because the business priority is catching as many churners as possible (highest churn recall, 0.66). Gradient Boosting has a slightly higher ROC-AUC and precision, so it is a reasonable alternative if precision matters more.

## Business impact
- **3,394 customers (17.0% of the test set)** are both high-risk and paying overage.
- They generate about **$140K/month** in overage revenue.
- If **30%** of them move to a stable plan instead of churning (an illustrative assumption, not a measured rate), that retains about **$42K/month** on the test set, or roughly **$210K/month** scaled to the full customer base.

## How to run
1. Open the notebook in Google Colab or Jupyter.
2. Place `Client.csv` and `Record.csv` in a Google Drive folder and update `DATA_PATH` in the notebook, or point it to a local folder.
3. Install dependencies: `pip install -r requirements.txt`
4. Run all cells.

## Repository contents
- `churn_overage_analysis.ipynb`: full analysis, from EDA to modelling and business sizing
- `requirements.txt`: Python dependencies

## Tech stack
Python, pandas, NumPy, scikit-learn, matplotlib, seaborn

## Author
**Anoushka Pramanik**
