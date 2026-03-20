# Education Dataset — Data Dictionary

## Overview
A large-scale synthetic dataset representing high school student records. The dataset captures academic performance, study habits, school environment, family background, and well-being indicators.

| Property | Value |
|----------|-------|
| Records | 300,000 |
| Columns | 22 |
| Date range | Jan 2022 – Sep 2024 |
| Target variables | 2 (1 classification, 1 regression) |

---

## Column Reference

### Student Profile

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `student_id` | String | Unique student identifier | — |
| `age` | Integer | Student age | Years |
| `gender` | Categorical | Student gender: Female, Male | — |

### Academic Metrics

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `gpa` | Float | Cumulative GPA | Scale 0–4 |
| `sat_score` | Integer | SAT test score | Score 600–1600 |
| `ap_courses_taken` | Integer | Number of AP courses completed | Count |
| `attendance_rate` | Float | Class attendance rate | Ratio (0–1) |

### Study Habits

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `study_hours_week` | Float | Average weekly study hours | Hours |
| `tutoring_hours` | Float | Weekly tutoring hours | Hours |
| `library_visits_week` | Integer | Library visits per week | Count |
| `online_resource_hours` | Float | Weekly hours using online resources | Hours |

### School Environment

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `school_type` | Categorical | School type: Public, Charter, Private | — |
| `class_size` | Integer | Average class size | Students |

### Family Background

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `family_income` | Float | Family annual income | USD |
| `parent_education` | Categorical | Highest parental education: No College, Some College, Bachelors, Graduate | — |

### Well-Being

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `extracurricular_count` | Integer | Number of extracurricular activities | Count |
| `discipline_incidents` | Integer | Discipline incidents on record | Count |
| `sleep_hours` | Float | Average nightly sleep | Hours |
| `stress_level` | Float | Self-reported stress level | Scale 1–10 |

### Temporal

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `enrollment_date` | Datetime | Date of enrollment | Date |

### Target Variables

| Column | Type | Description | Unit |
|--------|------|-------------|------|
| `academic_performance` | Integer | Performance level: 0 = High, 1 = Medium, 2 = Low | Class label |
| `college_readiness_score` | Float | College readiness index | Scale 10–100 |

---

## Suggested Starting Questions

**Classification — Academic Performance**

1. *Build a model to predict which students are at risk of low academic performance. What factors matter most, and how could a school counselor use this model for early intervention?*

2. *The school board wants to understand whether the drivers of academic success differ across school types and family backgrounds. Investigate this and recommend equitable support policies.*

**Regression — College Readiness Score**

3. *Develop a regression model to estimate college readiness scores. What combination of academic and non-academic factors best predicts readiness, and what does this suggest about holistic student development?*

4. *The district is evaluating tutoring and AP program effectiveness. Analyze whether students who use tutoring or take AP courses have higher readiness scores, controlling for other factors.*

---

## Data Quality Notes

This dataset contains intentional data quality challenges commonly found in real-world student information systems (SIS):

- **Missing values (~3%)** — Some fields have missing entries. The missingness is *not* random; it follows patterns that a careful analyst can identify.
- **Outliers (~0.2%)** — A small number of records contain extreme values that require investigation.
- **Entry errors (~5%)** — Some records contain implausible values that reflect real-world data-entry mistakes.

Students should plan a data-cleaning strategy **before** modeling.
