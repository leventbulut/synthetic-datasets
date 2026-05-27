# Exhibit B — Evergreen Retail Group Customer Analytics Dashboard

---

**Prepared by:** Customer Analytics Team
**Reporting Period:** Trailing 12 Months
**Data Source:** Consolidated CRM — Post-Acquisition Integration
**Record Date:** January 15

---

## Customer Base Overview

| Metric | Value |
|---|---|
| Total Transaction Records | 800,000 |
| Data Fields Captured | 22 |
| Source Systems Consolidated | 3 (Discount POS, Standard SaaS, Premium/Luxury Enterprise CRM) |
| Loyalty Program Members | 800,000 |

---

## Store Format Mix

| Store Format | Transaction Share | Avg. Transaction Amount | Avg. Customer Income |
|---|---|---|---|
| Discount | ~30% | Lower quartile | Below median |
| Standard | ~35% | Mid-range | Near median |
| Premium | ~25% | Upper-mid range | Above median |
| Luxury | ~10% | Highest | Top quartile |

> *Transaction shares are approximate. Students should compute exact distributions from the dataset. Average transaction amounts and income levels are described directionally — precise values should be derived from the data.*

---

## Product Category Revenue Shares

| Product Category | Approx. Share of Transactions |
|---|---|
| Grocery | 25% |
| Apparel | 20% |
| Electronics | 15% |
| Home & Garden | 15% |
| Beauty | 15% |
| Sports | 10% |

> *Grocery leads in transaction volume but may not lead in revenue per transaction. Students should investigate the relationship between category, average item price, and basket size.*

---

## Customer Demographics

| Metric | Value |
|---|---|
| Age Range | 16 – 85 years |
| Age Center | ~40 years |
| Gender Split | Female ~52%, Male ~48% |
| Income Center (z=0) | ~$29,674 |
| Income Range | ~$15,000 – $400,000 |

> *Income distribution shows meaningful right skew. A small population of high-income outliers may disproportionately influence mean-based statistics. Median income is a more robust central measure.*

---

## Customer Segment Distribution

| Segment | Code | Description |
|---|---|---|
| Budget | 0 | Price-sensitive, discount-driven shoppers |
| Moderate | 1 | Mainstream customers with moderate engagement |
| Premium | 2 | Higher-spend customers with strong loyalty |
| VIP | 3 | Highest-value, most engaged customers |

> ⚠️ *Segment assignments were inherited from legacy systems with different classification methodologies. The current distribution should be verified from the dataset. Cross-tabulation with store type, income, and CLV is recommended before modeling.*

---

## Customer Lifetime Value (CLV)

| Statistic | Value |
|---|---|
| Range | ~$20 – $15,000 |
| Distribution Shape | Log-normal (right-skewed) |

```
Distribution Shape (Illustrative):

  Freq
   ▓
   ▓▓
   ▓▓▓
   ▓▓▓▓▓
   ▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  ─────────────────────────────── CLV ($)
  $0    $2K    $4K    $6K    $8K   $10K+
         ↑median    ↑mean
```

> *The log-normal distribution means a small number of high-CLV customers contribute disproportionately to total value. Precise mean, median, and standard deviation should be computed from the dataset.*

---

## Satisfaction & Engagement

| Metric | Value |
|---|---|
| Satisfaction Score Range | 1 – 10 |
| Satisfaction Center | ~5.5 |

| Satisfaction Benchmark | Interpretation |
|---|---|
| 8.0 – 10.0 | Promoter / Advocate |
| 6.0 – 7.9 | Passively Satisfied |
| 4.0 – 5.9 | Indifferent / At-Risk |
| 1.0 – 3.9 | Dissatisfied / Detractor |

> *The company-wide average of approximately 5.5 falls in the "Indifferent / At-Risk" zone. Cross-tabulation by store format and customer segment is recommended.*

---

## Payment Method Distribution

| Payment Method | Approx. Share |
|---|---|
| Cash | ~25% |
| Debit | ~25% |
| Credit | ~25% |
| Mobile | ~25% |

> *Payment methods are approximately evenly distributed. Students should investigate whether payment preferences correlate with store format, customer segment, or CLV.*

---

## Referral Source Distribution

| Referral Source | Approx. Share |
|---|---|
| Walk-in | ~25% |
| Advertisement | ~25% |
| Online | ~25% |
| Referral | ~25% |

> *Referral sources are approximately evenly distributed. Differences in CLV or segment membership across referral channels may reveal acquisition quality insights.*

---

## Data Quality Summary

| Metric | Value |
|---|---|
| Total Data Cells | ~17.6 million (800,000 × 22) |
| Records with Missing Values | ~24,000 (~3%) |
| Records with Entry Errors | ~40,000 (~5%) |
| Records with Extreme Outliers | ~1,600 (~0.2%) |
| Affected Fields (Missing) | 5 columns |

> ⚠️ *Missingness is NOT random — it follows patterns linked to the legacy system origins. Entry errors include negative temporal values, physically implausible basket sizes, and extreme visit frequencies. A column-level audit is strongly recommended before modeling.*

---

## Key Questions for Q1 Strategic Planning

1. **VIP Realignment:** The manager-curated VIP list overlaps only 40% with data-driven CLV rankings. How should the $4.2M personalization program be restructured?
2. **Segmentation Model:** Can a 4-class classification system replace or supplement store-manager judgment for customer segmentation?
3. **CLV Prediction:** Can regression models produce reliable enough CLV estimates to set personalization investment thresholds?
4. **Data Integrity:** Are the ~24,000 missing records and ~40,000 entry errors distributed in ways that could bias segmentation or CLV models?
5. **Ethical Targeting:** Should income and store-type variables be used in segmentation models if they create differential service experiences across socioeconomic groups?

---

## Data Resources for Analysis

| Resource | Location |
|---|---|
| Transaction Dataset | `datasets/retail/synthetic_retail_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/retail_dictionary.md` |
| Suggested Analysis Tasks | `documentation/suggested_tasks/retail_tasks.md` |

---

*This dashboard is a fictional business document prepared for case discussion. All statistics are directionally consistent with the case dataset and should be independently verified by students as part of their exploratory data analysis.*
