# EXHIBIT B

## Precision Dynamics — Quality & Operations Dashboard Summary

---

**PRECISION DYNAMICS LLC**
**Quality Engineering Division — Operations Dashboard**

**Prepared by:** Priya Sharma, Data Analyst, Finance & Operations
**Date:** March 10, 2025
**Data Period:** January 2022 – September 2024

---

### 1. Dataset Overview

| Metric | Value |
|--------|-------|
| Total production batch records | 400,000 |
| Data fields per record | 21 |
| Date range | Jan 2022 – Sep 2024 |
| Product lines | 4 (Electronics, Automotive, Consumer Goods, Industrial) |
| Shifts | 3 (Day, Evening, Night) |
| Target variables | 2 (quality level, production cost) |

---

### 2. Production Volume by Product Line

| Product Line | Batch Count | Approx. Share |
|--------------|-------------|---------------|
| Automotive | ~120,000–140,000 | 30–35% |
| Consumer Goods | ~100,000–120,000 | 25–30% |
| Electronics | ~80,000–100,000 | 20–25% |
| Industrial | ~40,000–60,000 | 10–15% |
| **Total** | **400,000** | **100%** |

```
Production Volume by Line

Automotive      ████████████████████████████████▌       30–35%
Consumer Goods  ██████████████████████████▌             25–30%
Electronics     ████████████████████▌                   20–25%
Industrial      ████████████▌                           10–15%
```

---

### 3. Production Volume by Shift

| Shift | Batch Count | Approx. Share |
|-------|-------------|---------------|
| Day | ~160,000 | ~40% |
| Evening | ~120,000 | ~30% |
| Night | ~120,000 | ~30% |
| **Total** | **400,000** | **100%** |

> **Note:** The Day shift accounts for the largest share of production volume. Evening and Night shifts run approximately equal batch counts but with different staffing profiles (see Section 6).

---

### 4. Quality Level Distribution (Classification Target)

| Quality Level | Code | Approx. Share |
|---------------|------|---------------|
| High | 0 | ~8–12% |
| Medium | 1 | ~15–20% |
| Low | 2 | ~68–77% |
| **Total** | | **100%** |

```
Quality Level Distribution

High    ██████████▏                                           ~8–12%
Medium  ████████████████▌                                     ~15–20%
Low     ██████████████████████████████████████████████████████ ~68–77%
```

> **Analyst note:** The distribution is heavily skewed toward Low quality. Any classification model must account for this severe imbalance. A naïve model that predicts "Low" for every batch would achieve high accuracy but provide zero operational value.

---

### 5. Production Cost Distribution (Regression Target)

| Statistic | Value |
|-----------|-------|
| Center (typical batch) | ~$2,400 |
| Range | $50 – $100,000 |
| Distribution shape | Log-normal (right-skewed) |

> **Interpretation:** The long right tail reflects high-volume, complex batches — particularly on the Automotive and Industrial lines. The majority of batches cluster between $500 and $8,000, but cost outliers above $50,000 are present and must be investigated before modeling.

---

### 6. Operator Experience Summary

| Statistic | Value |
|-----------|-------|
| Center | ~6.0 years |
| Range | 0.5 – 35 years |

**Experience by Shift (Preliminary Observation):**

| Shift | Avg. Operator Experience |
|-------|--------------------------|
| Day | Higher than facility average |
| Evening | Near facility average |
| Night | Lower than facility average |

> **Analyst note:** The shift-experience correlation reflects the facility's seniority-based rotation policy. Junior operators are disproportionately assigned to Night shifts. This staffing pattern is a potential confound in any quality model that includes both shift and experience as features.

---

### 7. Machine Age Distribution

| Statistic | Value |
|-----------|-------|
| Center | ~4.5 years |
| Range | 0.5 – 25 years |

> **Note:** The IT correction script (described in the data quality section below) affected approximately 20,000 machine age records. Some values in the 40–80 year range remain in the dataset and require investigation.

---

### 8. Environmental & Process Parameter Ranges

| Parameter | Center | Range | Unit |
|-----------|--------|-------|------|
| Temperature | ~65 | 30 – 120 | °C |
| Humidity | ~45 | 15 – 90 | % |
| Vibration level | ~2.7 | 0.1 – 15 | mm/s |
| Power consumption | ~245 | 50 – 2,000 | kW |
| Cycle time | ~33 | 5 – 200 | sec |
| Batch size | ~403 | 50 – 20,000 | units |

> **Note:** The "Range" column reflects the expected operational envelope. Approximately 800 records (~0.2%) contain sensor values outside these ranges (e.g., temperatures above 200°C, vibration above 30 mm/s, power above 5,000 kW). These are suspected sensor malfunctions or transmission errors.

---

### 9. Quality & Material Metrics

| Metric | Center | Range |
|--------|--------|-------|
| Defect rate | ~0.14 | 0.001 – 0.15 |
| Supplier quality index | ~70 | 30 – 100 |

---

### 10. Data Quality Summary

| Issue Category | Estimated Scope | Status |
|----------------|-----------------|--------|
| Missing sensor values (vibration, temperature, humidity, power, defect rate) | ~12,000 records (~3%) | Under investigation — suspected link to maintenance mode |
| Physically impossible sensor readings | ~800 records (~0.2%) | Flagged — sensor malfunction or transmission error |
| Plausible-but-wrong entry errors (machine age, downtime, cycle time) | ~20,000 records (~5%) | Under investigation — includes IT script artifacts |

> **Note on missingness:** Missing values are concentrated in sensor fields and are not uniformly distributed across shifts, product lines, or time periods. Preliminary review suggests the MES does not record sensor data during maintenance windows, creating structured missingness.

> **Note on entry errors:** The IT correction script that ran on ~20,000 machine age records introduced an unknown number of plausible-but-incorrect values. Separately, approximately 20,000 records contain implausible downtime (500–1,500 minutes) and cycle time (500–1,200 seconds) values consistent with unit-of-measure confusion or shift-total vs. batch-level entry errors.

---

### 11. Preliminary Observations

1. **Severe class imbalance in quality level:** With 68–77% of batches classified as Low, the prediction challenge is identifying the minority High and Medium classes — not the majority.

2. **Log-normal cost distribution:** Standard regression on raw production cost will be dominated by the right tail. Log-transformation or robust regression methods are recommended.

3. **Shift–experience confound:** The seniority-based rotation policy creates a structural correlation between shift assignment and operator experience. Any model that includes both features must account for this relationship.

4. **Structured missingness:** The concentration of missing values in sensor fields — rather than random scatter across the dataset — suggests a systematic cause tied to equipment state. Understanding this pattern is a prerequisite for choosing an imputation strategy.

5. **Multi-layer data quality issues:** The dataset contains at least three distinct categories of quality problems (missing, impossible, plausible-but-wrong), each requiring a different remediation approach.

---

*Dashboard generated from Precision Dynamics MES Analytics Platform. Data refreshed March 8, 2025. For internal use only — do not distribute to external parties without Quality Engineering approval.*
