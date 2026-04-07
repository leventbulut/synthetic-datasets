# Depression Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing patient records from a mental-health screening and treatment programme. The dataset captures demographics, clinical history, validated screening instruments (PHQ-9, GAD-7), lifestyle and behavioural metrics, social factors, and treatment engagement.

| Property | Value |
|----------|-------|
| Records | 400,000 |
| Columns | 32 |
| Date range | Jan 2022 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Patient Demographics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `patient_id` | String | Unique patient identifier (DP0000001 format) | — |
| `age` | Integer | Patient age at screening | Years |
| `gender` | Categorical | Gender: Female, Male, Non-binary | — |
| `marital_status` | Categorical | Marital status: Single, Married, Divorced, Widowed | — |
| `education_level` | Categorical | Highest education: Less than High School, High School, Some College, Bachelor, Graduate | — |
| `employment_status` | Categorical | Employment: Unemployed, Part-time, Full-time, Student, Retired | — |
| `occupation` | Categorical | Occupation Sector / industry role | — |
| `annual_income` | Float | Annual household income | USD |

### Clinical History

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `prior_episodes` | Integer | Number of prior depressive episodes | Count |
| `family_history` | Categorical | Family history of depression: Yes, No | — |
| `chronic_conditions` | Integer | Number of comorbid chronic conditions | Count |
| `trauma_history` | Categorical | History of significant trauma: Yes, No | — |

### Screening Instruments

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `phq9_score` | Integer | Patient Health Questionnaire-9 depression score | Score 0–27 |
| `gad7_score` | Integer | Generalized Anxiety Disorder-7 score | Score 0–21 |

### Lifestyle & Behaviour

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `sleep_hours` | Float | Average nightly sleep duration | Hours |
| `sleep_quality` | Float | Self-reported sleep quality | Scale 1–10 |
| `exercise_days_week` | Integer | Days per week with 30+ min exercise | Days |
| `alcohol_drinks_week` | Integer | Alcoholic drinks consumed per week | Count |
| `substance_use` | Categorical | Current substance use: Yes, No | — |
| `screen_time_hours` | Float | Average daily screen time | Hours |
| `appetite_change` | Categorical | Appetite change: Normal, Decreased, Increased | — |

### Social Factors

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `social_support_score` | Float | Perceived social support | Scale 1–10 |
| `social_activity_days` | Integer | Days with social activity in last 2 weeks | Days |
| `isolation_index` | Float | Social isolation measure | Ratio (0–1) |
| `relationship_quality` | Float | Quality of close relationships | Scale 1–10 |

### Treatment

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `therapy_sessions_month` | Integer | Therapy sessions per month | Count |
| `medication_adherence` | Float | Medication adherence rate | Ratio (0–1) |
| `treatment_duration_months` | Float | Total months in treatment | Months |
| `on_medication` | Categorical | Currently prescribed antidepressants: Yes, No | — |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `screening_date` | Datetime | Date of screening assessment | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `depression_severity` | Integer | Depression severity: 0 = None/Mild, 1 = Moderate, 2 = Severe | Class label |
| `recovery_score` | Float | Treatment response / recovery progress | Scale 5–100 |

---

## Suggested Starting Questions

**Classification — Depression Severity**

1. *Can you build a model that predicts depression severity level from screening data? Which clinical and lifestyle factors are most informative, and how would a clinician use this model to triage patients for intensive treatment?*

2. *The mental health team suspects that depression severity profiles differ by age group and employment status. Investigate whether risk factors vary across subgroups and propose a targeted screening strategy.*

**Regression — Recovery Score**

3. *Develop a regression model to predict a patient's recovery score. What combination of treatment engagement, social factors, and clinical history best predicts treatment response?*

4. *The programme director wants to identify patients who are likely to respond poorly to current treatment. Build a recovery prediction model and identify patient profiles where the model is least accurate — what does this suggest about unmet treatment needs?*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world mental-health screening systems:

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
