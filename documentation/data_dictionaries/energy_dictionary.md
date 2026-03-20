# Energy Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing energy consumption records for buildings across residential, commercial, industrial, and institutional sectors. The dataset captures building characteristics, equipment data, weather conditions, and energy usage patterns.

| Property | Value |
|----------|-------|
| Records | 350,000 |
| Columns | 21 |
| Date range | Jan 2022 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Building Profile

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `record_id` | String | Unique measurement record ID | — |
| `building_type` | Categorical | Building category: Residential, Commercial, Industrial, Institutional | — |
| `building_age_years` | Integer | Age of building | Years |
| `floor_area_sqm` | Integer | Total floor area | m² |
| `num_occupants` | Integer | Number of regular occupants | Count |

### Systems & Equipment

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `insulation_rating` | Float | Building insulation quality score | Scale 15–100 |
| `hvac_age_years` | Float | Age of HVAC system | Years |
| `window_efficiency` | Float | Window thermal efficiency | Ratio (0–1) |
| `solar_panel_capacity_kw` | Float | Installed solar panel capacity | kW |
| `appliance_count` | Integer | Number of major appliances | Count |
| `smart_meter` | Categorical | Smart meter installed: Yes, No | — |
| `energy_source` | Categorical | Primary energy source: Natural Gas, Electricity, Mixed, Renewable | — |

### Maintenance

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `maintenance_frequency` | Integer | Maintenance visits per year | Count |
| `peak_demand_kw` | Float | Peak power demand | kW |

### Weather Conditions

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `outdoor_temp_c` | Float | Outdoor temperature at time of reading | °C |
| `humidity_pct` | Float | Outdoor relative humidity | Percent |
| `wind_speed_kmh` | Float | Wind speed at time of reading | km/h |
| `daylight_hours` | Float | Daylight hours on reading date | Hours |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `reading_date` | Datetime | Date of energy reading | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `efficiency_level` | Integer | Efficiency classification: 0 = High, 1 = Medium, 2 = Low | Class label |
| `energy_consumption_kwh` | Float | Total energy consumption | kWh |

---

## Suggested Starting Questions

**Classification — Efficiency Level**

1. *Build a model to classify buildings by energy efficiency level. Which building characteristics are most predictive, and how could a facilities manager use this model to prioritize retrofit investments?*

2. *The sustainability team suspects that efficiency drivers differ between building types. Investigate whether residential and commercial buildings require different improvement strategies.*

**Regression — Energy Consumption**

3. *Develop a regression model to predict monthly energy consumption. What factors have the largest impact on usage, and how should building operators adjust operations to reduce waste?*

4. *The utility company is considering a solar incentive program. Analyze how solar panel capacity relates to consumption and efficiency, and identify which building profiles would benefit most from subsidies.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world building management systems (BMS):

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
