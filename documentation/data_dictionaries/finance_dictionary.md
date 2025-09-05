# Finance Dataset Data Dictionary

## Overview
This dataset contains 750,000 synthetic customer records for financial services analysis, including credit risk assessment, fraud detection, and customer behavior analysis.

## Column Descriptions

### Customer Demographics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_id | int64 | Unique customer identifier | - | 0.00% |
| age | int64 | Customer age in years | years | 0.00% |
| income_level | category | Income category (Low, Medium, High, Very High) | - | 0.00% |
| education_level | category | Education attainment (High School, Bachelor, Master, PhD) | - | 0.00% |
| employment_status | category | Current employment status | - | 0.00% |
| credit_score | int64 | FICO credit score | score | 0.00% |

### Financial Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| annual_income | float64 | Annual income amount | USD | 0.01% |
| credit_limit | float64 | Total credit limit across all accounts | USD | 0.00% |
| total_debt | float64 | Total outstanding debt | USD | 0.00% |
| debt_to_income_ratio | float64 | Ratio of debt to annual income | ratio | 0.98% |
| credit_utilization | float64 | Percentage of credit limit used | percentage | 0.98% |
| payment_history_score | float64 | Score based on payment timeliness | score | 1.00% |

### Account Behavior
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| account_age_months | int64 | Age of oldest account in months | months | 0.00% |
| num_credit_cards | int64 | Number of active credit cards | count | 0.00% |
| num_loans | int64 | Number of active loans | count | 0.00% |
| avg_monthly_payment | float64 | Average monthly payment amount | USD | 0.02% |
| late_payments_90d | int64 | Number of payments 90+ days late | count | 0.00% |
| recent_inquiries | int64 | Credit inquiries in last 6 months | count | 0.00% |

### Temporal Features
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_since | datetime64[ns] | Date customer opened first account | date | 0.00% |
| last_activity_date | datetime64[ns] | Date of last account activity | date | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| credit_risk_level | category | Credit risk classification (Low, Medium, High, Very High) | - | 0.00% |
| fraud_risk_score | float64 | Fraud risk probability score | probability | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `payment_history_score` for customers with poor credit scores
- **Business Logic**: Customers with low credit scores may have incomplete payment histories

### Outliers (0.2%)
- **Income Outliers**: Very high income values (>$500k) and very low income values (<$5k)
- **Credit Score Outliers**: Extremely low scores (<300) and perfect scores (850)
- **Debt Outliers**: Unusually high debt-to-income ratios (>10)

### Entry Errors (≤30%)
- **Age Errors**: Some customers show unrealistic ages (<18 or >100)
- **Income Errors**: Inconsistent income levels vs. employment status
- **Date Errors**: Some future dates in customer_since field

## Target Variable Dependencies

### Credit Risk Level (Classification)
Depends on:
1. **credit_score** - Primary predictor (negative correlation)
2. **debt_to_income_ratio** - High ratio increases risk
3. **payment_history_score** - Poor payment history increases risk
4. **credit_utilization** - High utilization indicates risk
5. **late_payments_90d** - Recent late payments increase risk
6. **income_level** - Lower income associated with higher risk

### Fraud Risk Score (Regression)
Depends on:
1. **recent_inquiries** - Multiple inquiries may indicate fraud
2. **payment_history_score** - Sudden changes in payment behavior
3. **credit_utilization** - Unusual utilization patterns
4. **account_age_months** - New accounts may have higher fraud risk
5. **income_level** vs **credit_limit** - Mismatch may indicate fraud
