# EXHIBIT B

## Lakeview Unified School District — Student Analytics Dashboard Summary

---

**LAKEVIEW UNIFIED SCHOOL DISTRICT**
**Office of Data Analytics — Student Population Dashboard**

**Prepared by:** Dr. Carmen Reyes, Chief Data Officer
**Date:** Third week of March
**Data Period:** January 2022 – September 2024

---

### 1. Dataset Overview

| Metric | Value |
|--------|-------|
| Total student records | 300,000 |
| Data fields per record | 22 |
| Date range | Jan 2022 – Sep 2024 |
| School types represented | 3 (Public, Charter, Private) |
| Target variables | 2 (academic performance, college readiness score) |

---

### 2. Enrollment by School Type

| School Type | Student Count | Percentage |
|-------------|---------------|------------|
| Public | 149,832 | 49.9% |
| Charter | 90,264 | 30.1% |
| Private | 59,904 | 20.0% |
| **Total** | **300,000** | **100.0%** |

> **Note:** Public schools serve the largest share of the district's student population. Charter and Private schools enroll a disproportionate share of students from higher-income families, a pattern that has implications for cross-school-type modeling.

---

### 3. Student Demographics

| Gender | Count | Percentage |
|--------|-------|------------|
| Female | 156,000 | 52.0% |
| Male | 144,000 | 48.0% |
| **Total** | **300,000** | **100.0%** |

**Age Distribution:**

| Statistic | Value |
|-----------|-------|
| Mean | ~20 years |
| Range | 16 – 30 years |
| Peak concentration | 18 – 22 years |

---

### 4. Academic Performance Distribution (Classification Target)

| Performance Level | Code | Student Count | Percentage |
|-------------------|------|---------------|------------|
| High | 0 | — | — |
| Medium | 1 | — | — |
| Low | 2 | — | — |
| **Total** | | **300,000** | **100.0%** |

```
Academic Performance Distribution

High     ██████████████████████████████████                        
Medium   ██████████████████████████████████████████                
Low      ████████████████████████████                              
```

> **Analyst note:** The exact distribution across the three tiers is part of the team's exploratory analysis. The classification target uses 0 = High, 1 = Medium, 2 = Low. The distribution and relative sizes of each class should be assessed carefully before model training.

---

### 5. College Readiness Score Distribution (Regression Target)

| Statistic | Value |
|-----------|-------|
| Mean | ~40 |
| Range | 10 – 100 |
| Base center | 40 (pre-adjustment) |

> **Interpretation:** The college readiness score clusters in the lower-to-middle portion of the scale, with a concentration of students in the 20–50 range. A right tail of high-scoring students exists, but the majority of the district's students score below what many postsecondary institutions consider "college ready." This distribution is consistent with the eight-point enrollment decline cited by the superintendent.

---

### 6. GPA Distribution

| Statistic | Value |
|-----------|-------|
| Mean | 2.8 |
| Expected scale | 0.0 – 4.0 |
| Observed range | 0.5 – 6.0* |

```
GPA Distribution (Expected Range: 0–4)

0.5–1.0  ██▌                                                     
1.0–1.5  ████▌                                                   
1.5–2.0  ████████▌                                               
2.0–2.5  █████████████▌                                          
2.5–3.0  ████████████████████▌                                   
3.0–3.5  ██████████████████▌                                     
3.5–4.0  ████████████▌                                           
4.0+     ███▌ *                                                  
```

> *\*Records with GPA > 4.0 are suspected entry errors from the SIS migration. Lakeview uses an unweighted 0–4 scale. Approximately 5% of records contain at least one implausible value across GPA, class size, or discipline incidents.*

---

### 7. SAT Score Distribution

| Statistic | Value |
|-----------|-------|
| Mean | 1,050 |
| Expected range | 600 – 1,600 |
| Observed range | 50 – 1,600* |

> *\*A small number of records (< 0.2%) contain SAT scores below the modern test minimum of 400. These are suspected entry errors or legacy records from a prior scoring system.*

---

### 8. Attendance Rate

| Statistic | Value |
|-----------|-------|
| Mean | ~0.69 |
| Expected range | 0.50 – 0.99 |
| Distribution shape | Sigmoid-centered |

> **Observation:** The mean attendance rate of approximately 69% is lower than the district's publicly reported average of 82%. This discrepancy warrants investigation — it may reflect differences between how the SIS records attendance versus how the district reports it, or it may indicate that the dataset captures a broader definition of attendance (including partial-day absences).

---

### 9. Family Income Distribution

| Statistic | Value |
|-----------|-------|
| Mean | ~$36,315 |
| Median | — (to be confirmed) |
| Expected range | $15,000 – $400,000 |
| Observed range | $15,000 – $3,000,000* |
| Missing values | ~9,000 records across income and other fields |

> *\*Approximately 600 records contain family income values exceeding $800,000, with a handful above $2,000,000. These are flagged as statistical outliers pending investigation.*

> **Note on missingness:** Family income is one of several fields with missing values. The analytics team is investigating whether missingness in this field correlates with school type, student demographics, or other variables.

---

### 10. Parent Education Distribution

| Education Level | Approximate Share |
|-----------------|-------------------|
| No College | ~25% |
| Some College | ~25% |
| Bachelors | ~25% |
| Graduate | ~25% |

> **Note:** Parent education is roughly uniformly distributed across the four categories, though the analytics team is still verifying whether this distribution holds consistently across school types.

---

### 11. Study Habits & Well-Being Summary

| Variable | Mean | Range |
|----------|------|-------|
| Study hours/week | ~12.2 | 1 – 50* |
| Sleep hours/night | 7.0 | 4 – 10 |
| Stress level (self-reported) | 5.0 | 1 – 10 |
| Class size | 25 | 10 – 45** |

> *\*Approximately 600 records show study hours/week exceeding 60, with some above 100. These are flagged as outliers.*
> *\*\*Approximately 15,000 records contain class sizes between 60 and 150 — suspected data-entry errors from the SIS migration.*

---

### 12. Data Quality Summary

| Issue Category | Scope |
|----------------|-------|
| Missing values (across 6 fields) | ~9,000 records (~3%) |
| Suspected entry errors (GPA, class size, discipline) | ~15,000 records (~5%) |
| Statistical outliers (SAT, income, study hours) | ~600 records (~0.2%) |

> **Note on missingness:** Missing values are concentrated in six columns: `family_income`, `sat_score`, `study_hours_week`, `attendance_rate`, `sleep_hours`, and `stress_level`. Preliminary review suggests the missingness is not random. A formal missingness analysis is underway.

> **Note on entry errors:** The SIS migration did not enforce upper-bound validation on several numeric fields. Entry errors are most prevalent in `class_size`, `discipline_incidents`, and `gpa`. A comprehensive data quality audit is recommended before model development.

---

### 13. Feature Categories

The 22 data fields are organized into the following categories:

| Category | Fields | Examples |
|----------|--------|----------|
| Student Profile | 3 | student_id, age, gender |
| Academic Metrics | 4 | gpa, sat_score, ap_courses_taken, attendance_rate |
| Study Habits | 4 | study_hours_week, tutoring_hours, library_visits_week, online_resource_hours |
| School Environment | 2 | school_type, class_size |
| Family Background | 2 | family_income, parent_education |
| Well-Being | 4 | extracurricular_count, discipline_incidents, sleep_hours, stress_level |
| Temporal | 1 | enrollment_date |
| Targets | 2 | academic_performance, college_readiness_score |

---

### 14. Preliminary Observations

1. **College readiness concentration in the lower range:** The majority of students score below 50 on the 10–100 readiness scale, consistent with the enrollment decline that prompted the initiative.

2. **GPA data quality:** The presence of GPAs above 4.0 is a clear SIS migration artifact. The team must decide whether to cap, impute, or remove these records — each choice has downstream modeling implications.

3. **Income as a signal:** Even in preliminary cross-tabulations, family income shows a strong association with both academic performance and college readiness. This signal is analytically valuable and ethically complex.

4. **Missing data patterns:** The concentration of missing values in specific columns — rather than random scatter — suggests a systematic cause tied to the SIS migration or inconsistent data collection practices across school types.

5. **Attendance discrepancy:** The gap between the SIS-recorded mean attendance rate (~69%) and the district's publicly reported rate (82%) requires reconciliation before attendance can be used as a reliable model feature.

---

*Dashboard generated from Lakeview SIS Analytics Platform. Data refreshed third week of March. For internal use only — not for public distribution.*
