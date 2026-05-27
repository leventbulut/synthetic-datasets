# Exhibit B — Meridian Wireless Subscriber Dashboard

**Period: January 2021 – December 2024 | Prepared by: Office of the SVP, Customer Retention**

---

## Section 1: Subscriber Overview

### 1.1 Base Summary

| Metric | Value |
|--------|-------|
| **Total Active Subscribers** | 550,000 |
| **Date Range** | January 2021 – December 2024 |
| **Number of Variables Captured** | 22 |
| **Mean Subscriber Age** | 42 years |
| **Age Range** | 18–85 years |
| **Median Tenure** | ~20 months |
| **Tenure Range** | 1–180 months |

### 1.2 Plan Mix

| Plan Type | Description | Approx. Monthly Charge Range |
|-----------|-------------|------------------------------|
| Basic | Voice + limited data | $20–$40 |
| Standard | Voice + moderate data + SMS | $35–$75 |
| Premium | Unlimited voice/data + add-ons | $70–$150 |
| Enterprise | Business accounts, multi-line | $100–$300 |

The Basic and Standard tiers account for the majority of the subscriber base. Enterprise subscribers represent a smaller segment by headcount but contribute disproportionately to revenue.

### 1.3 Contract Type Distribution

| Contract Type | Description |
|---------------|-------------|
| Month-to-month | No commitment; highest flexibility, highest churn exposure |
| One year | Moderate commitment; standard retention terms |
| Two year | Longest commitment; lowest churn, highest acquisition cost |

Month-to-month subscribers comprise the largest single contract segment. This is the primary source of churn volume and the segment most affected by competitive switching offers.

---

## Section 2: Financial Profile

### 2.1 Monthly Charge Distribution

| Metric | Value |
|--------|-------|
| **Center (approx.)** | ~$45 |
| **Range** | $20–$300 |
| **Distribution** | Right-skewed (log-normal) |

The distribution is right-skewed: the typical subscriber pays meaningfully less than the arithmetic mean, which is pulled upward by Premium and Enterprise accounts. Cost analysis should use median-based measures for "typical" subscriber economics.

### 2.2 Retention Spend (Last Quarter)

| Item | Amount |
|------|--------|
| Total retention credits issued | $4,200,000 |
| Subscribers receiving retention offers | 58,900 |
| Average credit per offer | $71.30 |
| Estimated % of credits to low-risk subscribers | ~40% |
| Estimated wasted retention spend | ~$1,680,000 |

---

## Section 3: Usage Patterns

### 3.1 Data Usage

| Metric | Value |
|--------|-------|
| **Center (approx.)** | ~12 GB/month |
| **Range** | 0.5–200 GB |
| **Distribution** | Right-skewed (log-normal) |

Heavy data users (>50 GB/month) represent a small but growing segment, driven by streaming, remote work, and mobile hotspot usage.

### 3.2 Voice Minutes

| Metric | Value |
|--------|-------|
| **Center (approx.)** | ~245 minutes/month |
| **Range** | 10–3,000 minutes |
| **Distribution** | Right-skewed (log-normal) |

Voice usage varies substantially by age cohort, with older subscribers and Enterprise accounts driving the upper tail.

### 3.3 SMS Count

| Metric | Value |
|--------|-------|
| **Note** | SMS data affected by billing migration; ~5% of records contain implausible values |

SMS counts should be treated with caution pending data quality review. The legacy-to-cloud billing migration corrupted a subset of records, producing counts that exceed reasonable usage patterns.

---

## Section 4: Service Quality Metrics

### 4.1 Network Reliability

| Metric | Value |
|--------|-------|
| **Center (approx.)** | ~0.92 (uptime ratio) |
| **Range** | 0.80–0.999 |
| **Distribution** | Left-skewed (sigmoid-compressed) |

The majority of subscribers experience reliability above 0.90, but a meaningful tail extends below this threshold. Subscribers with reliability below 0.90 warrant engineering review and may represent coverage gaps in specific geographic areas.

### 4.2 Average Download Speed

| Metric | Value |
|--------|-------|
| **Center (approx.)** | ~33 Mbps |
| **Range** | 5–200 Mbps |

Download speed varies by plan tier (Basic plans are speed-capped), geographic location, and network congestion patterns.

### 4.3 Customer Service Interactions

| Metric | Description |
|--------|-------------|
| **Customer Service Calls** | Calls to support in last 6 months |
| **Complaint Count** | Formal complaints in last 12 months |

High service call volume is a known churn signal across the industry. However, ~5% of customer service call records contain entry errors (implausible counts) from the billing migration.

---

## Section 5: Billing & Payment

### 5.1 Payment Method Distribution

| Payment Method | Description |
|----------------|-------------|
| Paper check | Traditional mail-in payment |
| Electronic check | Online ACH/e-check payment |
| Bank transfer | Direct bank-to-Meridian transfer |
| Credit card | Card-on-file autopay |

### 5.2 Paperless Billing

| Status | Description |
|--------|-------------|
| Yes | Subscriber receives statements electronically |
| No | Subscriber receives paper statements by mail |

Approximately half of the subscriber base has enrolled in paperless billing. Enrollment correlates with age, payment method, and digital engagement.

---

## Section 6: Churn Risk Profile

### 6.1 Churn Classification Distribution

| Risk Category | Label | Description |
|---------------|-------|-------------|
| Retain | 0 | Low churn risk — stable, engaged subscriber |
| At Risk | 1 | Moderate churn risk — behavioral warning signals present |
| Likely Churn | 2 | High churn risk — strong indicators of impending departure |

The three-class distribution should be examined carefully. Understanding the relative size of each class and its relationship to contract type, payment method, and tenure is essential for both model design and retention strategy.

### 6.2 Satisfaction Score

| Metric | Value |
|--------|-------|
| **Center** | ~5.5 |
| **Range** | 1–10 |
| **Survey Completion Rate** | ~30% |

With only 30% of subscribers completing satisfaction surveys, the satisfaction data has inherent selection bias: subscribers who respond may not be representative of the full base. The regression model should account for this limitation.

---

## Section 7: Data Quality Summary

### 7.1 Known Issues

| Issue Type | Estimated Prevalence | Primary Cause |
|------------|---------------------|---------------|
| Missing values | ~16,500 records (~3%) | Billing system migration gaps |
| Entry errors | ~27,500 records (~5%) | Legacy data conversion artifacts |
| Outliers | ~1,100 records (~0.2%) | Extreme but potentially valid usage |

### 7.2 Affected Fields

Missing values are concentrated in a subset of columns rather than distributed uniformly. The missingness is **not random** — it follows patterns related to the billing migration timeline and subscriber characteristics. Analysts should investigate the structure of missingness before choosing an imputation strategy.

### 7.3 Implications for Analytics

- Models built on this data must account for systematic missingness and entry errors.
- Naive imputation (e.g., mean substitution) may introduce bias if applied to non-randomly missing fields.
- Model validation should assess whether performance differs across subscriber segments where data quality varies.

---

## Section 8: Strategic Questions for the Customer Committee

1. **Retention ROI:** At $4.2M per quarter in retention spend with a rising churn rate, what is the break-even point for a model-driven retention program? How much waste can targeted intervention eliminate?

2. **Targeting Ethics:** If the strongest churn predictors are proxies for age and digital literacy, how should Meridian design retention campaigns that are both effective and non-discriminatory?

3. **Satisfaction as Leading Indicator:** Can predicted satisfaction scores serve as an early warning system for churn? Or are satisfaction and churn driven by different factors?

4. **Data Investment:** What improvements to billing system data capture, CRM integration, and survey methodology would improve the quality and coverage of subscriber analytics?

---

*All figures in this dashboard are derived from the Meridian Wireless subscriber extract (550,000 records, 22 columns). This document is prepared for internal planning purposes and case study discussion.*
