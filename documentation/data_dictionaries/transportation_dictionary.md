# Transportation Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing delivery operations for a logistics company. The dataset captures route characteristics, driver metrics, vehicle data, environmental conditions, and delivery outcomes.

| Property | Value |
|----------|-------|
| Records | 450,000 |
| Columns | 22 |
| Date range | Jan 2022 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Delivery Details

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `delivery_id` | String | Unique delivery identifier | — |
| `distance_km` | Float | Total delivery distance | km |
| `load_weight_kg` | Float | Total cargo weight | kg |
| `num_stops` | Integer | Number of delivery stops | Count |
| `priority_level` | Categorical | Delivery priority: Standard, Express, Same Day | — |

### Vehicle & Driver

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `vehicle_type` | Categorical | Vehicle type: Bike, Van, Truck, Heavy Truck | — |
| `driver_experience_years` | Float | Driver experience | Years |
| `fuel_efficiency` | Float | Vehicle fuel efficiency | km/L |
| `maintenance_score` | Float | Vehicle maintenance quality score | Scale 30–100 |
| `driver_rating` | Float | Customer rating of driver | Scale 1–5 |

### Route & Conditions

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `route_type` | Categorical | Route type: Urban, Suburban, Highway | — |
| `weather_condition` | Categorical | Weather: Clear, Rain, Snow, Fog | — |
| `traffic_density` | Float | Traffic congestion level | Ratio (0–1) |

### Duration & Performance

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `planned_duration_hours` | Float | Planned delivery duration | Hours |
| `actual_duration_hours` | Float | Actual delivery duration | Hours |
| `delay_minutes` | Integer | Delivery delay | Minutes |
| `fuel_cost` | Float | Total fuel cost for delivery | USD |
| `package_condition` | Categorical | Package arrival condition: Perfect, Good, Minor Damage, Damaged | — |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `dispatch_date` | Datetime | Date of dispatch | Date |
| `delivery_date` | Datetime | Date of delivery | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `delivery_success` | Integer | Delivery outcome: 0–2 | Class label |
| `delivery_cost` | Float | Total delivery cost | USD |

---

## Suggested Starting Questions

**Classification — Delivery Success**

1. *Build a model to predict delivery outcomes. Which factors most influence whether a delivery arrives on time, and how could dispatchers use this model to identify at-risk shipments before they leave?*

2. *The fleet manager believes that driver experience and vehicle maintenance interact to affect on-time performance. Investigate this relationship and propose a driver-vehicle pairing strategy.*

**Regression — Delivery Cost**

3. *Develop a regression model to estimate delivery costs. What are the main cost drivers, and how could the company use this model for dynamic pricing of delivery services?*

4. *The company wants to reduce fuel costs. Analyze the relationship between route type, vehicle type, and fuel efficiency, and recommend fleet optimization strategies.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world fleet management systems (TMS):

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
