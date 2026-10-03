# Customer Churn & Revenue Intelligence

End-to-end customer churn analysis in Python: identifying what drives customers to leave, predicting who is at risk, and estimating the revenue that retention actions could protect.

## Business Problem

A telecom subscription business is losing about **one in three customers (33.8%)**. Leadership needs to know:

1. Where is the churn coming from?
2. How much revenue does it cost?
3. Which active customers should the retention team contact first?

## Dataset

2,000 customers with demographics, contract and billing details, and churn status.

| Column group | Fields |
|---|---|
| Customer | Customer ID, name, gender, age, city |
| Service | Contract type, internet service, signup date |
| Billing | Monthly charges, total charges, tenure (months) |
| Target | Churn (Yes / No / Unknown) |

Churn rate is calculated as `Yes / (Yes + No)`. The 35 customers with unknown churn status are excluded. Imputation flags and a data-quality log are included in the dataset.

## Approach

1. **Data preparation:** cleaned column names, removed unused columns, created age groups, handled missing and unknown values.
2. **Exploratory analysis:** 10 business questions on churn by contract, tenure, age, internet service, city and signup cohort, plus revenue impact.
3. **Statistical testing:** chi-square tests and Cramer's V to check which factors are significantly linked to churn.
4. **Predictive modelling:** Logistic Regression and Random Forest, evaluated with ROC-AUC, confusion matrix and cross-validation.
5. **Risk scoring:** out-of-fold churn probabilities for every active customer, grouped into Low / Medium / High risk bands.
6. **Scenario analysis:** revenue saved under different churn-reduction targets.

## Key Findings

- **Overall churn is 33.8%** (665 of 1,965 customers with known status), costing about **Rs 5.67 lakh in monthly revenue (about Rs 68 lakh a year)**.
- **Contract type is the strongest driver.** Month-to-month customers churn at **47.8%**, versus 20.2% for one-year and 10.9% for two-year contracts. Month-to-month customers account for about 78% of all churn.
- **The first year is the danger zone.** About half of all churn happens within 12 months; churn falls to 8.6% for customers with 49+ months of tenure.
- **Fiber customers churn the most (37.7%)** and account for about 63% of lost revenue, largely because many are on month-to-month plans.
- **Age, city and gender are not statistically significant** (p-values 0.39 to 0.88).
- **Newer signups churn far more:** 46.1% for the 2025 cohort versus 4 to 12% for 2019-2021 cohorts.

## Predictive Model

| Model | ROC-AUC (test) |
|---|---|
| Logistic Regression | 0.75 |
| Random Forest | 0.75 |

- Cross-validated ROC-AUC is about 0.71.
- The model identifies **84% of customers who actually churn** (recall), at 51% precision, a reasonable trade-off for a retention campaign.
- Among 1,300 active customers, **178 are High risk**, representing about **Rs 1.80 lakh in monthly revenue**.

## Recommendations

1. **Move month-to-month customers to 1- or 2-year plans** with targeted incentives. A 20% reduction in month-to-month churn is worth about **Rs 10.5 lakh a year**.
2. **Run retention outreach from the risk-scored call list,** starting with the High-risk band.
3. **Strengthen onboarding and check-ins during the first 6 to 12 months.**
4. **Review Fiber service quality and pricing,** since it is the most valuable and highest-churn segment.
5. **Investigate acquisition quality for the 2024-2025 cohorts.**

## Limitations

- The model uses only four features (tenure, monthly charges, contract, internet service), so it should be used to prioritise customers, not as a precise forecast.
- The data is a single snapshot, so tenure and signup-cohort effects are partly intertwined.
- Usage, complaint and payment history data would likely improve predictions.

## Repository Structure

```
.
├── churn_portfolio_project.ipynb   # Full analysis notebook
├── clean_customer_data_2000.xlsx   # Dataset
├── requirements.txt                # Python dependencies
└── README.md
```

## How to Run

```bash
git clone https://github.com/<your-username>/customer-churn-revenue-intelligence.git
cd customer-churn-revenue-intelligence
pip install -r requirements.txt
jupyter notebook churn_portfolio_project.ipynb
```

Keep the Excel file in the same folder as the notebook, then choose **Kernel > Restart & Run All**.

## Tech Stack

Python, pandas, NumPy, matplotlib, seaborn, SciPy, scikit-learn, Jupyter

## Author

**<Himanshi>**
[LinkedIn](https://www.linkedin.com/in/<himanshii5809>) | [GitHub](https://github.com/<himanshii5809-analyst>)
