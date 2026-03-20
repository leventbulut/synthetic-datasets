# Healthcare Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing patient encounters at a multi-facility hospital system. The dataset captures patient demographics, admission details, vital signs, lab values, clinical metrics, and insurance information.

| Property | Value |
|----------|-------|
| Records | 500,000 |
| Columns | 21 |
| Date range | Jan 2022 – Jun 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Patient Demographics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `patient_id` | String | Unique patient identifier (HC0000001 format) | — |
| `age` | Integer | Patient age at admission | Years |
| `gender` | Categorical | Patient gender: M, F | — |

### Admission Details

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `admission_type` | Categorical | Type of admission: Elective, Urgent, Emergency, Trauma | — |
| `primary_diagnosis` | Categorical | Primary diagnosis category: Orthopedic, Gastrointestinal, Respiratory, Cardiovascular, Neurological | — |
| `hospital_department` | Categorical | Treating department: Pediatrics, General Medicine, Emergency, Cardiology, Surgery, ICU | — |
| `length_of_stay` | Integer | Total days in hospital | Days |

### Vital Signs

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `systolic_bp` | Float | Systolic blood pressure at admission | mmHg |
| `diastolic_bp` | Float | Diastolic blood pressure at admission | mmHg |
| `heart_rate` | Float | Heart rate at admission | BPM |
| `temperature` | Float | Body temperature at admission | °F |

### Lab Values

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `hemoglobin` | Float | Hemoglobin level from blood panel | g/dL |
| `creatinine` | Float | Creatinine level from blood panel | mg/dL |
| `glucose` | Float | Blood glucose level | mg/dL |

### Clinical Metrics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `comorbidity_count` | Integer | Number of comorbid conditions | Count |
| `medication_count` | Integer | Number of active medications | Count |

### Insurance

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `insurance_type` | Categorical | Insurance coverage: Self-Pay, Other, Private, Medicaid, Medicare | — |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `admission_date` | Datetime | Date of hospital admission | Date |
| `discharge_date` | Datetime | Date of hospital discharge | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `readmission_risk` | Integer | Readmission risk: 0 = Low, 1 = Medium, 2 = High | Class label |
| `total_cost` | Float | Total cost of hospital stay | USD |

---

## Suggested Starting Questions

**Classification — Readmission Risk**

1. *Can you build a model that predicts which patients are at high risk of readmission within 30 days? Which performance metric matters most — overall accuracy or catching high-risk patients — and how does this affect your model choice?*

2. *Hospital administrators believe certain diagnosis categories and departments drive higher readmission rates. Investigate whether readmission risk varies systematically across clinical factors and propose targeted interventions.*

**Regression — Total Cost**

3. *Develop a regression model to estimate the total cost of a patient's hospital stay. What are the most important cost drivers, and how could the hospital use this model for budget planning?*

4. *The CFO is concerned about cost variability. Build a cost prediction model and identify patient profiles where cost is hardest to predict. What does this tell the hospital about where to focus process improvement?*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world EHR systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
