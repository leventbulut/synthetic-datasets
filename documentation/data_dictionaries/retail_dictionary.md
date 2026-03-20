# Retail Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing customer transactions at a multi-format retail chain. The dataset captures demographics, purchase behavior, loyalty program activity, and channel preferences.

| Property | Value |
|----------|-------|
| Records | 800,000 |
| Columns | 22 |
| Date range | Jan 2021 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Customer Demographics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `transaction_id` | String | Unique transaction identifier | — |
| `age` | Integer | Customer age | Years |
| `gender` | Categorical | Customer gender: Female, Male | — |
| `annual_income` | Float | Customer annual income | USD |

### Store & Product

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `store_type` | Categorical | Store format: Discount, Standard, Premium, Luxury | — |
| `product_category` | Categorical | Product category: Electronics, Apparel, Grocery, Home & Garden, Beauty, Sports | — |

### Purchase Behavior

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `basket_size` | Integer | Number of items per transaction | Count |
| `avg_item_price` | Float | Average price per item | USD |
| `transaction_amount` | Float | Total transaction value | USD |
| `visit_frequency_monthly` | Integer | Store visits per month | Count |
| `days_since_last_visit` | Integer | Days since last store visit | Days |

### Loyalty & Engagement

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `loyalty_member` | Categorical | Loyalty program member: Yes, No | — |
| `loyalty_points` | Integer | Accumulated loyalty points | Points |
| `online_purchase_pct` | Float | Fraction of purchases made online | Ratio (0–1) |
| `return_rate` | Float | Product return rate | Ratio (0–1) |
| `discount_sensitivity` | Float | Responsiveness to discounts | Ratio (0–1) |
| `satisfaction_score` | Float | Customer satisfaction survey score | Scale 1–10 |
| `referral_source` | Categorical | How customer was acquired: Walk-in, Advertisement, Online, Referral | — |

### Payment

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `payment_method` | Categorical | Payment type: Cash, Debit, Credit, Mobile | — |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `transaction_date` | Datetime | Date of transaction | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `customer_segment` | Integer | Customer segment: 0–3 | Class label |
| `customer_lifetime_value` | Float | Predicted customer lifetime value | USD |

---

## Suggested Starting Questions

**Classification — Customer Segment**

1. *Build a model to classify customers into segments. What distinguishes a VIP customer from a Budget one, and how would a store manager use this classification to personalize service?*

2. *The merchandising team wants to understand whether segmentation patterns differ across store types and product categories. Investigate this and recommend category-specific strategies.*

**Regression — Customer Lifetime Value**

3. *Develop a regression model to predict customer lifetime value. What behaviors drive long-term value, and how should the loyalty program be redesigned to increase CLV?*

4. *The e-commerce team wants to grow online sales. Analyze the relationship between online purchase percentage and CLV, and recommend strategies to shift high-value customers to digital channels.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world POS and CRM systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
