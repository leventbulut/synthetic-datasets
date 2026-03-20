# Manufacturing Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing production batch records from a multi-line manufacturing facility. The dataset captures machine parameters, environmental conditions, operator metrics, and quality outcomes.

| Property | Value |
|----------|-------|
| Records | 400,000 |
| Columns | 21 |
| Date range | Jan 2022 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Production Identity

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `record_id` | String | Unique production record ID | — |
| `product_line` | Categorical | Product line: Electronics, Automotive, Consumer Goods, Industrial | — |
| `batch_size` | Integer | Units produced in the batch | Count |
| `shift` | Categorical | Production shift: Day, Evening, Night | — |

### Machine & Operator

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `machine_age_years` | Float | Age of production machine | Years |
| `operator_experience` | Float | Operator experience level | Years |

### Process Conditions

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `temperature_c` | Float | Production environment temperature | °C |
| `humidity_pct` | Float | Production environment humidity | Percent |
| `vibration_level` | Float | Machine vibration intensity | mm/s |
| `power_consumption` | Float | Machine power draw during production | kW |
| `cycle_time_sec` | Float | Average cycle time per unit | Seconds |

### Quality & Materials

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `defect_rate` | Float | Batch defect rate | Ratio (0–1) |
| `scrap_rate` | Float | Material scrap rate | Ratio (0–1) |
| `raw_material_cost` | Float | Raw material cost per unit | USD |
| `supplier_quality_index` | Float | Incoming material quality score | Scale 30–100 |

### Maintenance

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `maintenance_hours` | Float | Maintenance hours in last 30 days | Hours |
| `downtime_minutes` | Integer | Unplanned downtime during batch | Minutes |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `production_date` | Datetime | Date of production | Date |
| `inspection_date` | Datetime | Date of quality inspection | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `quality_level` | Integer | Quality classification: 0 = High, 1 = Medium, 2 = Low | Class label |
| `production_cost` | Float | Total production cost for the batch | USD |

---

## Suggested Starting Questions

**Classification — Quality Level**

1. *Build a model to predict batch quality level. Which process parameters are most important for maintaining high quality, and what thresholds would you recommend for real-time monitoring?*

2. *The quality engineering team suspects that machine age and operator experience interact to affect quality outcomes. Investigate this relationship and propose a predictive maintenance schedule.*

**Regression — Production Cost**

3. *Develop a regression model to estimate production cost per batch. What are the main cost drivers, and where should the operations team focus to reduce costs without compromising quality?*

4. *The plant manager wants to optimize shift scheduling. Analyze whether production costs and quality vary by shift, and build a model that accounts for shift-level effects.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world MES (Manufacturing Execution Systems):

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
