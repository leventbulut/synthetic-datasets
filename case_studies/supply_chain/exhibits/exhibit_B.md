# Exhibit B — Vanguard Manufacturing Global Procurement Dashboard

**Period: ~4 Years of Procurement Data | Prepared by: Procurement Analytics, Office of the VP of Global Procurement**

---

## Section 1: Procurement Overview

### 1.1 Portfolio Summary

| Metric | Value |
|--------|-------|
| Total Purchase Orders | 1,000,000 |
| Data Fields Captured | 22 |
| Product Categories | 4 |
| Supplier Regions | 4 |
| Shipping Methods | 4 |
| Order Priority Levels | 4 (Low, Medium, High, Critical) |

### 1.2 Total Cost Profile

| Metric | Value |
|--------|-------|
| **Distribution** | Log-normal |
| **Center (Mode Region)** | ~$1,808 |
| **Typical Range** | $2,000 – $15,000 |
| **Minimum (Clipped)** | $100 |
| **Maximum (Clipped)** | $500,000 |

The log-normal distribution of total cost means that the bulk of orders cluster in a relatively narrow band, but a long right tail of high-value orders has an outsized impact on procurement budgets. Understanding what drives orders into that tail is critical for budget forecasting and variance management.

---

## Section 2: Supplier Performance Metrics

### 2.1 Composite Supplier Rating

| Metric | Value |
|--------|-------|
| Mean Rating | ~50 |
| Range | 10 – 100 |
| Interpretation | Higher = better overall performance |

### 2.2 Compliance Score

| Metric | Value |
|--------|-------|
| Mean Score | ~60 |
| Range | 20 – 100 |
| Interpretation | Regulatory and quality compliance composite |

### 2.3 On-Time Delivery Rate

| Metric | Value |
|--------|-------|
| Distribution | Sigmoid-shaped |
| Range | 0.30 – 0.99 |
| Interpretation | Proportion of orders delivered by expected date |

### 2.4 Defect Rate

| Metric | Value |
|--------|-------|
| Distribution | Sigmoid-shaped |
| Range | 0.001 – 0.20 |
| Interpretation | Proportion of units with quality defects |

**Key Observation:** Supplier rating (mean ~50) and compliance score (mean ~60) both sit near the midpoint of their respective scales, suggesting significant variation across the supplier base. The on-time delivery range of 0.30 to 0.99 indicates that some suppliers deliver on time less than a third of the time — a level of performance that would trigger remediation at most manufacturers.

---

## Section 3: Order Characteristics

### 3.1 Order Quantity

| Metric | Value |
|--------|-------|
| Median | ~665 units |
| Range | 10 – 50,000 units |

### 3.2 Unit Price

| Metric | Value |
|--------|-------|
| Median | ~$12.18 |
| Range | $1 – $500 |

### 3.3 Lead Time

| Metric | Value |
|--------|-------|
| Median | ~12 days |
| Range | 1 – 90 days |

### 3.4 Product Category Mix

| Category | Description |
|----------|-------------|
| Raw Materials | Base inputs — metals, chemicals, polymers |
| Components | Manufactured subassemblies and precision parts |
| Packaging | Containers, wrapping, labeling materials |
| Finished Goods | Completed products sourced for resale or integration |

Each category carries distinct risk and cost profiles. Components, for example, tend to involve specialized suppliers with longer qualification cycles and higher switching costs — as the KHPC failure demonstrated.

### 3.5 Order Priority Distribution

| Priority | Description |
|----------|-------------|
| Low | Routine replenishment, flexible delivery window |
| Medium | Standard production schedule, moderate urgency |
| High | Near-term production need, limited buffer |
| Critical | Immediate production impact, expedited handling required |

---

## Section 4: Logistics Profile

### 4.1 Shipping Methods

| Method | Typical Use Case |
|--------|-----------------|
| Sea | High-volume, long-distance, cost-optimized |
| Rail | Continental freight, moderate speed and cost |
| Road | Regional delivery, flexible routing |
| Air | Urgent/critical orders, highest cost |

### 4.2 Warehouse & Inventory

| Metric | Value |
|--------|-------|
| Warehouse Utilization — Mean | ~50% |
| Warehouse Utilization — Range | 20% – 98% |
| Inventory Turnover — Median | ~4.5 turns/year |

A median inventory turnover of 4.5 turns per year is within the typical range for diversified industrial manufacturers, but the variation around this figure warrants investigation. Low-turnover SKUs may represent excess inventory tying up working capital; high-turnover items with thin safety stock buffers are candidates for stockout risk.

---

## Section 5: Supplier Risk Distribution

### 5.1 Risk Classification

| Risk Level | Class | Description |
|------------|-------|-------------|
| Minimal | 0 | Strong performance history, low disruption probability |
| Low | 1 | Acceptable performance, minor concerns |
| Moderate | 2 | Elevated risk, active monitoring recommended |
| High/Critical | 3 | Significant risk, remediation or contingency required |

**Key Observation:** The High/Critical tier (Class 3) represents the most populated class at roughly 55–60% of all records. This concentration raises strategic questions: Is the supplier base genuinely high-risk, or does the classification methodology need recalibration? Either answer has significant implications for procurement strategy.

### 5.2 Supplier Regions

| Region | Markets |
|--------|---------|
| Asia | China, Japan, South Korea, Taiwan, Southeast Asia |
| Europe | EU member states, UK, Turkey |
| North America | United States, Canada, Mexico |
| South America | Brazil, Argentina, Chile, Colombia |

Vanguard's supplier base spans four major regions, each with distinct regulatory environments, logistics infrastructure, trade compliance requirements, and risk profiles. The interaction between supplier region and risk classification is a critical analytical question — and a sensitive one.

---

## Section 6: Data Quality Summary

### 6.1 Missing Values

| Metric | Value |
|--------|-------|
| Records with Missing Values | ~30,000 |
| Overall Missing Rate | ~3% of affected fields |
| Distribution | Not random — concentrated in supplier performance fields |

### 6.2 Known Data Quality Issues

| Issue Type | Estimated Prevalence | Likely Source |
|------------|---------------------|---------------|
| Missing values | ~30,000 records (~3%) | Staggered ERP rollout, regional data capture gaps |
| Entry errors | ~50,000 records (~5%) | Manual entry during ERP transitions |
| Outliers | ~2,000 records (~0.2%) | Extreme but potentially valid procurement events |

**Context:** Vanguard's ERP system was implemented in stages across regions over a two-year period. Each regional rollout involved different implementation teams, different validation rules, and different levels of staff training. The data quality issues are not uniform — they reflect the history of the system's deployment.

### 6.3 Implications for Analytics

- Supplier performance fields (ratings, defect rates, compliance scores, on-time delivery, return rates) have the highest missingness rates. These are precisely the fields most important for risk modeling.
- The ~50,000 entry errors in lead time, payment terms, and stockout frequency are distinguishable from legitimate values by domain knowledge — implausible values exceed operational norms by wide margins.
- Any model built on this data must document its cleaning strategy and assess whether performance degrades for subgroups where data quality is poorest.

---

## Section 7: Strategic Questions for the Operations Committee

1. **Concentration Risk:** What percentage of procurement volume flows through High/Critical-risk suppliers? Is this an acceptable level of exposure?

2. **Geographic Diversification:** Should Vanguard rebalance its supplier base across regions to reduce concentration risk, even if it increases short-term costs?

3. **Cost Visibility:** Can total order cost be predicted accurately enough at the time of order placement to meaningfully improve budget forecasting?

4. **Data Infrastructure:** What investments in ERP data governance, supplier performance monitoring, and real-time analytics are needed to sustain a predictive risk management program?

5. **Bias vs. Intelligence:** If the risk model shows regional variation in supplier risk, how should Vanguard distinguish legitimate supply chain intelligence from historical procurement bias?

---

*All figures in this dashboard are derived from the Vanguard Manufacturing ERP extract (1,000,000 purchase order records). This document is prepared for internal planning purposes and case study discussion.*
