# Supply Chain Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing procurement and logistics transactions for a multi-national manufacturer. The dataset captures product orders, supplier performance, shipping logistics, and inventory metrics.

| Property | Value |
|----------|-------|
| Records | 1,000,000 |
| Columns | 22 |
| Date range | Jan 2021 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Order Details

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `order_id` | String | Unique order identifier | — |
| `product_category` | Categorical | Product type: Raw Materials, Components, Packaging, Finished Goods | — |
| `order_quantity` | Integer | Items ordered | Count |
| `unit_price` | Float | Price per unit | USD |
| `lead_time_days` | Integer | Days from order to delivery | Days |
| `order_priority` | Categorical | Priority level: Low, Medium, High, Critical | — |

### Supplier Performance

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `on_time_delivery_rate` | Float | Historical on-time delivery rate | Ratio (0–1) |
| `defect_rate` | Float | Historical defect rate | Ratio (0–1) |
| `supplier_rating` | Float | Composite supplier quality score | Scale 10–100 |
| `supplier_region` | Categorical | Supplier location: Asia, Europe, North America, South America | — |
| `compliance_score` | Float | Regulatory compliance score | Scale 20–100 |

### Logistics & Inventory

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `shipping_method` | Categorical | Transport mode: Sea, Rail, Road, Air | — |
| `warehouse_utilization` | Float | Warehouse capacity in use | Ratio (0–1) |
| `inventory_turnover` | Float | Annual inventory turns | Turns/year |
| `stockout_frequency` | Integer | Stockout events in last 12 months | Count |
| `return_rate` | Float | Product return rate | Ratio (0–1) |
| `shipping_cost` | Float | Shipping cost for the order | USD |
| `payment_terms_days` | Integer | Net payment terms | Days |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `order_date` | Datetime | Date order was placed | Date |
| `expected_delivery_date` | Datetime | Expected delivery date | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `supplier_risk` | Integer | Supplier risk level: 0–3 | Class label |
| `total_cost` | Float | Total order cost | USD |

---

## Suggested Starting Questions

**Classification — Supplier Risk**

1. *Build a model to classify suppliers by risk level. Which supplier attributes are most predictive, and how would procurement use this to pre-qualify vendors?*

2. *The VP of Operations suspects that supplier risk varies significantly by region and product category. Investigate this and recommend a diversification strategy.*

**Regression — Total Cost**

3. *Develop a regression model to estimate total order cost. What drives cost variability, and how could the company use this model for accurate purchase-order budgeting?*

4. *The logistics team wants to reduce shipping costs. Build a cost model and identify which order characteristics offer the most potential for cost savings.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world ERP systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
