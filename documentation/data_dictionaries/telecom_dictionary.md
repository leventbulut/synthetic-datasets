# Telecommunications Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing subscribers at a mobile and broadband provider. The dataset captures demographics, plan details, usage metrics, service quality, and billing patterns.

| Property | Value |
|----------|-------|
| Records | 550,000 |
| Columns | 22 |
| Date range | Jan 2021 – Dec 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Subscriber Profile

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `customer_id` | String | Unique subscriber identifier | — |
| `age` | Integer | Subscriber age | Years |
| `tenure_months` | Integer | Months as an active subscriber | Months |

### Plan & Contract

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `plan_type` | Categorical | Service plan: Basic, Standard, Premium, Enterprise | — |
| `monthly_charge` | Float | Monthly bill amount | USD |
| `contract_type` | Categorical | Contract term: Month-to-month, One year, Two year | — |
| `payment_method` | Categorical | Payment method: Paper check, Electronic check, Bank transfer, Credit card | — |
| `paperless_billing` | Categorical | Paperless billing: Yes, No | — |

### Usage

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `data_usage_gb` | Float | Monthly data consumption | GB |
| `call_minutes` | Integer | Monthly voice minutes used | Minutes |
| `sms_count` | Integer | Monthly SMS messages sent | Count |
| `num_add_on_services` | Integer | Number of active add-on services | Count |

### Service Quality

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `network_reliability` | Float | Network uptime ratio | Ratio (0–1) |
| `avg_download_speed` | Float | Average download speed | Mbps |
| `customer_service_calls` | Integer | Service calls in last 6 months | Count |
| `complaint_count` | Integer | Formal complaints in last 12 months | Count |

### Loyalty

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `referral_count` | Integer | Friends/family referred | Count |
| `late_payment_count` | Integer | Late payments in last 12 months | Count |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `signup_date` | Datetime | Date of initial subscription | Date |
| `last_activity_date` | Datetime | Date of most recent account activity | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `churn_prediction` | Integer | Churn classification: 0–2 | Class label |
| `satisfaction_score` | Float | Customer satisfaction survey result | Scale 1–10 |

---

## Suggested Starting Questions

**Classification — Churn Prediction**

1. *Build a churn prediction model. Which subscriber behaviors are the strongest early warning signals, and how far in advance can you reliably predict churn?*

2. *The retention team has a limited budget for targeted offers. Investigate whether churn drivers differ between plan types and contract lengths, and recommend segment-specific retention strategies.*

**Regression — Satisfaction Score**

3. *Develop a regression model to predict customer satisfaction scores. What aspects of service quality matter most, and which operational improvements would yield the biggest satisfaction gains?*

4. *The product team is considering new add-on services. Analyze the relationship between current add-ons, usage patterns, and satisfaction. Which customer profiles would benefit most from new offerings?*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world telecom billing and CRM systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
