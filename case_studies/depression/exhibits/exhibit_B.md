# EXHIBIT B

## BrightPath Community Mental Health Network — Analytics Dashboard Summary

---

**BRIGHTPATH ANALYTICS DIVISION**
**Network Performance Dashboard — Data Summary**

**Prepared by:** Marcus Chen, Director of Analytics
**Date:** March 3, 2025
**Data Period:** January 2022 – September 2024

---

### 1. Dataset Overview

| Metric | Value |
|--------|-------|
| Total patient screening records | 400,000 |
| Data fields per record | 32 |
| Date range | Jan 2022 – Sep 2024 |
| Number of clinics | 12 |
| Target variables | 2 (depression severity, recovery score) |

---

### 2. Clinical Screening Scores

| Instrument | Mean | Clinical Interpretation |
|------------|------|------------------------|
| PHQ-9 (Depression) | 10.3 | Moderate depression (scale 0–27) |
| GAD-7 (Anxiety) | 7.2 | Mild-moderate anxiety (scale 0–21) |

> **Note:** The PHQ-9 clinical thresholds are: 0–4 Minimal, 5–9 Mild, 10–14 Moderate, 15–19 Moderately Severe, 20–27 Severe. Our network-wide average of 10.3 places the typical BrightPath patient at the lower boundary of moderate depression.

---

### 3. Depression Severity Distribution (Classification Target)

| Severity Level | Code | Patient Count | Percentage |
|----------------|------|---------------|------------|
| None/Mild | 0 | 210,953 | 52.7% |
| Moderate | 1 | 76,142 | 19.0% |
| Severe | 2 | 112,905 | 28.2% |
| **Total** | | **400,000** | **100.0%** |

```
Severity Distribution

None/Mild  ████████████████████████████████████████████████████▋  52.7%
Moderate   ███████████████████▏                                  19.0%
Severe     ████████████████████████████▏                         28.2%
```

---

### 4. Recovery Score Distribution (Regression Target)

| Statistic | Value |
|-----------|-------|
| Mean | 76.3 |
| Median | 85.4 |
| Scale range | 5 – 100 |

> **Interpretation:** The gap between mean (76.3) and median (85.4) indicates a left-skewed distribution. The majority of patients achieve recovery scores above 80, but a substantial tail of patients shows very poor treatment response. This tail represents the population most at risk for treatment disengagement.

---

### 5. Patient Employment Profile

| Employment Status | Count | Percentage |
|-------------------|-------|------------|
| Full-time | 101,919 | 25.5% |
| Unemployed | 90,616 | 22.7% |
| Part-time | 79,561 | 19.9% |
| Retired | 69,933 | 17.5% |
| Student | 57,971 | 14.5% |
| **Total** | **400,000** | **100.0%** |

---

### 6. Occupation Breakdown (Employed Patients)

| Occupation Category | Patient Count |
|---------------------|---------------|
| Business Operations | 20,927 |
| Sales | 20,838 |
| Management | 20,788 |
| Education | 20,777 |
| Construction | 14,465 |
| Architecture & Engineering | 14,260 |
| Sciences | 14,172 |
| Food Preparation | 11,219 |
| Office & Administrative | 11,186 |
| Personal Care | 11,119 |
| Healthcare Support | 10,865 |
| Social Services | 10,864 |

> **Analyst note:** Occupation data is available only for patients reporting Full-time or Part-time employment. The distribution across sectors reflects the regional employment base. Further analysis by occupation subgroup is pending.

---

### 7. Data Quality Summary

| Issue Category | Scope |
|----------------|-------|
| Total missing values across dataset | ~12,000 |
| Missing values as % of total cells | ~0.09% of 12.8M cells |
| Suspected entry errors | Under investigation |
| Outlier records flagged | Under investigation |

> **Note on missingness:** Missing values are concentrated in a subset of columns. Preliminary review suggests that the missingness may not be random. The EMR migration in July 2023 may have introduced systematic gaps. A formal missingness analysis is underway.

> **Note on data entry:** Initial screening identified a small number of records with values that fall within valid ranges but appear clinically implausible when examined in context. A comprehensive data quality audit is recommended before model development.

---

### 8. Feature Categories

The 32 data fields are organized into the following categories:

| Category | Fields | Examples |
|----------|--------|----------|
| Patient Demographics | 8 | age, gender, employment status, occupation, income |
| Clinical History | 4 | prior episodes, family history, chronic conditions, trauma |
| Screening Instruments | 2 | PHQ-9 score, GAD-7 score |
| Lifestyle & Behaviour | 7 | sleep hours, exercise, alcohol, screen time |
| Social Factors | 4 | social support, isolation, relationship quality |
| Treatment | 4 | therapy sessions, medication adherence, duration |
| Temporal | 1 | screening date |
| Targets | 2 | depression severity, recovery score |

---

### 9. Preliminary Observations

1. **Class imbalance in severity:** The Moderate category (19.0%) is notably smaller than both None/Mild (52.7%) and Severe (28.2%). This may present challenges for multiclass classification, particularly in distinguishing Moderate from adjacent categories.

2. **Recovery score distribution:** The left skew warrants investigation. Standard regression approaches that assume normally distributed residuals may not be appropriate without transformation.

3. **Missing data patterns:** The concentration of missing values in specific columns — rather than random scatter across the dataset — suggests a systematic cause. Understanding this pattern is a prerequisite for choosing an appropriate imputation strategy.

4. **Employment and occupation data:** The rich occupation data presents both an analytical opportunity and an ethical consideration. The analytics team recommends a formal discussion of occupation-based features before model development begins.

---

*Dashboard generated from BrightPath Analytics Platform v3.2. Data refreshed March 1, 2025. For internal use only.*
