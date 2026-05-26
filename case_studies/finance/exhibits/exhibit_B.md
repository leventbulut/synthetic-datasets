# Exhibit B — Atlas National Bank Risk Dashboard

---

**ATLAS NATIONAL BANK**
*Enterprise Risk Management — Portfolio Composition Snapshot*

---

**Prepared by:** Risk Analytics Division
**Reporting Period:** Most Recent Quarter-End
**Data Source:** Enterprise Data Warehouse — Post-Merger Consolidated Extract
**Total Records:** 750,000 Active Consumer Accounts

---

## Portfolio Overview

| Metric | Value |
|---|---|
| Total Customer Records | 750,000 |
| Data Fields Captured | 23 |
| Source Systems Consolidated | 2 (Atlas Core, Lakeview Legacy) |
| Bank Total Assets | $28 Billion |

---

## Credit Score Distribution

| Range | Estimated Share | Risk Interpretation |
|---|---|---|
| 750 – 850 | ~20% | Prime / Super-Prime |
| 700 – 749 | ~22% | Near-Prime |
| 650 – 699 | ~25% | Core Middle |
| 600 – 649 | ~18% | Sub-Prime Transition |
| 300 – 599 | ~15% | Sub-Prime / Deep Sub-Prime |
| **Portfolio Mean** | **~680** | |
| **Portfolio Range** | **300 – 850** | |

```
Distribution Shape (Illustrative):

  Freq
   ▓▓
   ▓▓▓▓
   ▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  ──────────────────────────── Credit Score
  300   450   600   680  750   850
                     ↑mean
```

> ⚠️ *Approximately 1,500 records (~0.2%) contain credit scores in the 30–150 range — well below the standard FICO floor of 300. These are flagged as suspected entry errors pending investigation.*

---

## Employment Status Breakdown

| Employment Status | Estimated Share |
|---|---|
| Full-Time | ~30% |
| Part-Time | ~18% |
| Self-Employed | ~17% |
| Retired | ~20% |
| Unemployed | ~15% |

> *Employment distribution reflects post-merger portfolio composition. Unemployed segment shows disproportionate missingness in income and financial fields (~3% of total records affected).*

---

## Regional Exposure

| Region | Share of Portfolio | Legacy Source |
|---|---|---|
| Southeast | 25% | Primarily Lakeview |
| Northeast | 20% | Primarily Atlas |
| Midwest | 20% | Mixed |
| West | 20% | Primarily Atlas (expansion) |
| Southwest | 15% | Primarily Atlas (expansion) |

> *Southeast concentration increased from ~8% pre-merger to 25%. Regional default dynamics differ from the Northeast-trained legacy model's assumptions.*

---

## Education Profile

| Education Level | Estimated Share |
|---|---|
| High School | ~22% |
| Some College | ~21% |
| Bachelor's Degree | ~24% |
| Master's Degree | ~19% |
| PhD | ~14% |

---

## Key Financial Ratios

| Metric | Value |
|---|---|
| **Income** | |
| Median Income | ~$36,315 |
| Income Range | $22,000 – $550,000+ |
| Distribution Shape | Lognormal, right-skewed |
| **Credit Utilization** | |
| Portfolio Average | ~35% |
| **Debt-to-Income Ratio** | |
| Portfolio Average | ~32% |
| **Monthly Spending** | |
| Typical Range | $500 – $8,000 |
| Outlier Range | $80,000 – $250,000 (~0.2%) |

```
Income Distribution (Illustrative):

  Freq
   ▓
   ▓▓
   ▓▓▓▓
   ▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  ──────────────────────────── Income ($)
  $22K   $36K  $75K  $150K  $550K+
          ↑median
```

> *Mean income exceeds median, confirming right skew. A small but significant tail of high-net-worth clients (income > $200K) may disproportionately influence aggregate statistics.*

---

## Fraud Risk Score Profile

| Statistic | Value |
|---|---|
| Score Range (Clipped) | 0.01 – 12.0 |
| Typical Cluster | 0.19 – 1.0 |
| Distribution Shape | Right-skewed |

> *The majority of accounts score below 1.0. Scores above 3.0 represent < 5% of the portfolio but generate the majority of compliance review volume. Current thresholds have not been recalibrated since the merger.*

---

## Data Quality Summary

| Issue Category | Records Affected | Share of Portfolio |
|---|---|---|
| Missing Values | ~22,500 | ~3.0% |
| Entry Errors | ~37,500 | ~5.0% |
| Outliers | ~1,500 | ~0.2% |

| Data Quality Metric | Value |
|---|---|
| Total Data Cells | ~17.25 million (750,000 × 23) |
| Total Records with Issues | ~61,500 (some overlap) |
| Fields Most Affected (Missing) | Income, Investment Value, Savings Rate, Credit Utilization, Debt-to-Income, Monthly Spending |
| Fields Most Affected (Errors) | Employment Years, Num Credit Cards, Late Payment Months |
| Missingness Pattern | Non-random — concentrated among unemployed customers (MNAR suspected) |

> ⚠️ *Aggregate data quality issues affect approximately 8% of the portfolio. However, overlap between categories means the true number of unique affected records may be lower. A field-level audit is recommended before modeling begins. The OCC examiner will expect full documentation of data quality handling.*

---

## Key Questions for Stress Test Preparation

1. **Model Accuracy:** The legacy model predicted 2.1% defaults; actual was 3.8%. Can a rebuilt model on the full 750,000-record dataset close this gap?
2. **Credit Risk Classification:** Are the four-class risk labels (Very Low / Low / Medium / High) accurately distributed across the current portfolio?
3. **Fraud Triage:** Can the fraud risk scoring system be recalibrated to reduce false positives without increasing missed fraud?
4. **Data Integrity:** Are the ~22,500 missing values and ~37,500 entry errors randomly distributed or concentrated in ways that could bias the model?
5. **Fair Lending:** Do employment status and home ownership create disparate impact risk if included as model features?

---

## Data Resources for Analysis

| Resource | Location |
|---|---|
| Customer Dataset | `datasets/finance/synthetic_finance_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/finance_dictionary.md` |
| Suggested Analysis Tasks | `documentation/suggested_tasks/finance_tasks.md` |

---

*This dashboard is a fictional business document prepared for case discussion. All statistics are consistent with the case dataset and should be independently verified by students as part of their exploratory data analysis.*
