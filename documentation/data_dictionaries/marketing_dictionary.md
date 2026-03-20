# Marketing Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing digital customer interactions for a multi-channel e-commerce retailer. The dataset captures demographics, digital engagement, purchase behavior, and marketing response patterns across **600,000 customers**.

| Property | Value |
|----------|-------|
| Records | 600,000 |
| Columns | 29 |
| Date range | Jan 2021 – Dec 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Customer Demographics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `customer_id` | String | Unique customer identifier (MK0000001 format) | — |
| `age` | Integer | Customer age at time of data collection | Years |
| `income` | Float | Estimated annual household income | USD |
| `education_level` | Categorical | Highest education attained: *High School, Some College, Bachelors, Graduate* | — |
| `location_type` | Categorical | Primary residence area: *Urban, Suburban, Rural* | — |

### Digital Engagement

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `visit_frequency` | Integer | Website visits in the last 30 days | Count |
| `session_duration` | Float | Average time per website session | Minutes |
| `pages_per_session` | Integer | Average pages viewed per session | Count |
| `bounce_rate` | Float | Proportion of single-page sessions | Ratio (0–1) |
| `email_open_rate` | Float | Proportion of marketing emails opened | Ratio (0–1) |
| `email_click_rate` | Float | Proportion of marketing emails clicked | Ratio (0–1) |
| `social_engagement` | Integer | Social media interactions (likes, shares, comments) per month | Count |
| `mobile_usage` | Float | Monthly hours spent on the company's mobile app | Hours |

### Purchase & Loyalty

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `customer_segment` | Categorical | Loyalty tier: *Bronze, Silver, Gold, Platinum, Diamond* | — |
| `purchase_frequency` | Categorical | Purchase cadence: *Rare, Occasional, Regular, Frequent, Very Frequent* | — |
| `avg_order_value` | Float | Average dollar amount per order | USD |
| `days_since_last_purchase` | Integer | Days elapsed since the customer's most recent purchase | Days |
| `satisfaction_score` | Float | Most recent customer satisfaction survey result | Scale 1–10 |
| `support_contacts` | Integer | Customer support interactions in the last 6 months | Count |
| `discount_usage` | Integer | Number of discount/promo codes redeemed | Count |
| `referral_count` | Integer | Number of new customers referred | Count |
| `newsletter_months` | Integer | Duration of newsletter subscription | Months |

### Marketing & Channel

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `marketing_channel` | Categorical | Primary acquisition channel: *Email, Social Media, Search, Display, Affiliate* | — |
| `device_preference` | Categorical | Primary browsing device: *Desktop, Mobile, Tablet, Mixed* | — |
| `campaign_response_rate` | Float | Response rate to targeted marketing campaigns | Ratio (0–1) |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `registration_date` | Datetime | Date the customer first registered | Date |
| `last_activity_date` | Datetime | Date of the customer's most recent activity | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `churn_risk` | Integer | Churn risk classification: 0 = Low, 1 = Medium, 2 = High | Class label |
| `customer_lifetime_value` | Float | Predicted total customer value | USD |

---

## Suggested Starting Questions

**Classification — Churn Risk**

1. *Can you build a model that predicts which customers are at high risk of churning? Which evaluation metric would you prioritize — accuracy, precision, or recall — and why does it matter for a retention campaign?*

2. *The marketing team suspects that certain customer segments churn at very different rates. Investigate whether churn risk varies systematically across segments and propose a targeted intervention strategy.*

**Regression — Customer Lifetime Value**

3. *Develop a regression model to estimate customer lifetime value. How accurately can you predict CLV, and what does your model reveal about the most important drivers of long-term customer value?*

4. *The CFO wants to allocate next quarter's marketing budget proportionally to customer value. Build a CLV prediction pipeline, evaluate its reliability, and identify customer profiles where your model is least accurate.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world CRM systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values (e.g., negative durations, impossible ages) that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
