# Exhibit B — Lakeview Regional Medical Center Operational Dashboard

**Period: January 2022 – June 2024 | Prepared by: Office of the CFO**

---

## Section 1: Financial Overview

### 1.1 Cost per Patient Encounter

| Metric | Value |
|--------|-------|
| **Mean Total Cost** | $10,997 |
| **Median Total Cost** | $9,987 |
| **Standard Deviation** | $4,303 |
| **Cost Skew** | Right-skewed (mean > median by ~$1,010) |

The $1,010 gap between mean and median total cost indicates a right-skewed distribution: a subset of high-cost encounters pulls the average above the typical patient. The standard deviation of $4,303 — nearly 40% of the mean — reflects substantial cost variability across the patient population.

### 1.2 Financial Risk Exposure — CMS Penalty

| Item | Amount |
|------|--------|
| Estimated Annual Medicare Revenue | ~$140,000,000 |
| HRRP Penalty Rate | 3.00% |
| **Estimated Annual Penalty** | **$4,200,000** |

For context, the annual penalty exceeds the total cost of approximately 382 average-cost patient encounters. Alternatively, $4.2 million could fund a transitional care program serving thousands of high-risk patients annually.

---

## Section 2: Patient Census Summary

### 2.1 Total Volume

| Metric | Value |
|--------|-------|
| Total Patient Encounters | 500,000 |
| Date Range | January 2022 – June 2024 |
| Average Length of Stay | 5.8 days |
| Number of Variables Captured | 21 |

### 2.2 Admissions by Department

| Department | Encounters | % of Total |
|------------|-----------|------------|
| Pediatrics | 128,135 | 25.6% |
| ICU | 91,355 | 18.3% |
| General Medicine | 89,884 | 18.0% |
| Emergency | 81,010 | 16.2% |
| Cardiology | 59,992 | 12.0% |
| Surgery | 49,624 | 9.9% |
| **Total** | **500,000** | **100.0%** |

### 2.3 Admissions by Type

| Admission Type | Encounters | % of Total |
|----------------|-----------|------------|
| Elective | 158,274 | 31.7% |
| Urgent | 148,828 | 29.8% |
| Trauma | 96,719 | 19.3% |
| Emergency | 96,179 | 19.2% |
| **Total** | **500,000** | **100.0%** |

Elective and urgent admissions together represent 61.4% of all encounters. Non-elective pathways (trauma + emergency) account for 38.6%.

---

## Section 3: Clinical Profile

### 3.1 Primary Diagnosis Categories

The dataset captures five primary diagnosis categories:

- Orthopedic
- Gastrointestinal
- Respiratory
- Cardiovascular
- Neurological

Diagnosis-level cost and readmission variation should be examined to identify which clinical pathways carry the greatest financial and quality risk.

### 3.2 Insurance Mix

| Insurance Type | Description |
|----------------|-------------|
| Medicare | Federal program, primary payer for 65+ and disability |
| Medicaid | Federal/state program for low-income patients |
| Private | Employer-sponsored or individual market plans |
| Self-Pay | Uninsured / no third-party coverage |
| Other | Workers' comp, VA, TRICARE, etc. |

The insurance mix has direct implications for both revenue realization and readmission risk. Self-pay patients typically have lower reimbursement rates and may face barriers to post-discharge care access.

### 3.3 Readmission Risk Distribution

| Risk Level | Count | Percentage | Interpretation |
|------------|-------|------------|----------------|
| Low (0) | 263,357 | 52.7% | Standard discharge, routine follow-up |
| Medium (1) | 129,842 | 26.0% | Enhanced discharge planning recommended |
| High (2) | 106,801 | 21.4% | Intensive post-discharge intervention indicated |

**Key Concern:** The high-risk population (21.4%) represents over 106,000 patient encounters. If even a fraction of these patients are readmitted within 30 days, the cumulative impact on CMS penalty calculations is substantial.

---

## Section 4: Data Quality Summary

### 4.1 Missing Values

| Metric | Value |
|--------|-------|
| Total Missing Values | 14,996 |
| Total Data Points | 10,500,000 (500,000 × 21) |
| Overall Missing Rate | 0.14% |

While the overall missing rate is low, missingness is **not uniformly distributed** across columns. Certain clinical documentation fields show higher rates of missing data than administrative or demographic fields. This pattern may reflect documentation workflow differences across departments and time periods.

### 4.2 Known Data Quality Issues

| Issue Type | Estimated Prevalence | Source |
|------------|---------------------|--------|
| Missing values | ~3% of affected columns | EHR documentation gaps |
| Entry errors | ~5% of records | Manual data entry under time pressure |
| Outliers | ~0.2% of records | Extreme but potentially valid clinical values |

**Context:** The 2023–2024 nursing staffing crisis disproportionately affected Emergency Department documentation. Travel nurse onboarding did not include full EHR training, resulting in inconsistent charting practices during peak shortage months.

### 4.3 Implications for Analytics

- Any predictive model built on this data must account for missing values and potential entry errors.
- The non-random nature of missingness means that naive imputation (e.g., mean substitution) may introduce bias.
- Model validation should assess whether performance degrades for patient subgroups where data quality is lower.

---

## Section 5: Strategic Questions for the Board

1. **Investment vs. Penalty:** At $4.2M annually, how much should Lakeview invest in readmission reduction programs? What is the break-even point?

2. **Targeting:** Should post-discharge resources be allocated based on clinical risk factors alone, or should socioeconomic factors (including insurance status) inform resource allocation?

3. **Data Infrastructure:** What investments in EHR documentation training, data governance, and real-time analytics are needed to sustain a predictive modeling program?

4. **Timeline:** The next CMS measurement window includes discharges through June 2025. Is there enough time to implement interventions that will measurably reduce readmissions?

---

*All figures in this dashboard are derived from the Lakeview Regional Medical Center EHR extract (500,000 patient encounters). This document is prepared for internal planning purposes and case study discussion.*
