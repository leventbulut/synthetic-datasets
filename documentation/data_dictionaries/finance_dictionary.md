# Finance Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing customer profiles at a consumer bank. The dataset captures demographics, employment, credit behavior, account activity, and investment patterns.

| Property | Value |
|----------|-------|
| Records | 750,000 |
| Columns | 23 |
| Date range | Jan 2019 – Dec 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Customer Demographics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `customer_id` | String | Unique customer identifier (FN0000001 format) | — |
| `age` | Integer | Customer age | Years |
| `income` | Float | Annual household income | USD |
| `credit_score` | Integer | FICO credit score | Score 300–850 |
| `employment_years` | Float | Years with current employer | Years |
| `employment_status` | Categorical | Employment type: Unemployed, Part-time, Self-employed, Full-time, Retired | — |
| `education_level` | Categorical | Highest education: High School, Some College, Bachelor, Master, PhD | — |
| `marital_status` | Categorical | Marital status: Single, Married, Divorced, Widowed | — |
| `home_ownership` | Categorical | Home status: Rent, Mortgage, Own, Other | — |
| `region` | Categorical | Geographic region: Northeast, Southeast, Midwest, Southwest, West | — |

### Account & Credit Behavior

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `account_age_months` | Integer | Age of primary bank account | Months |
| `monthly_spending` | Float | Average monthly card spending | USD |
| `credit_utilization` | Float | Credit utilization ratio | Ratio (0–1) |
| `num_credit_cards` | Integer | Number of active credit cards | Count |
| `num_loans` | Integer | Number of active loans | Count |
| `late_payment_months` | Integer | Months with late payments in last 2 years | Count |
| `debt_to_income` | Float | Debt-to-income ratio | Ratio |
| `savings_rate` | Float | Savings rate as fraction of income | Ratio (0–1) |
| `investment_value` | Float | Total investment portfolio value | USD |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `account_creation_date` | Datetime | Date the primary account was created | Date |
| `last_transaction_date` | Datetime | Date of the most recent transaction | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `credit_risk` | Integer | Credit risk classification: 0–3 (Very Low to High) | Class label |
| `fraud_risk_score` | Float | Fraud risk index | Score |

---

## Suggested Starting Questions

**Classification — Credit Risk**

1. *Build a classification model to predict a customer's credit risk level. Which features are most predictive, and how would a loan officer use this model to make faster decisions?*

2. *The risk management team suspects that credit risk drivers differ across employment types and income brackets. Investigate this hypothesis and recommend segment-specific lending policies.*

**Regression — Fraud Risk Score**

3. *Develop a regression model to estimate a customer's fraud risk score. What behavioral patterns are associated with higher fraud risk, and how would you flag suspicious accounts?*

4. *The compliance team needs to prioritize account reviews. Build a fraud scoring pipeline and identify which customer profiles produce the most false positives. How would you reduce them?*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world banking CRM systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
