# Exhibit A — CEO Memorandum: Supplier Failure Post-Mortem & Board Mandate

**CONFIDENTIAL — EXECUTIVE TEAM DISTRIBUTION ONLY**

---

## Memorandum

**From:** Diana Cheng, Chief Executive Officer
**To:** Executive Leadership Team
**CC:** Board of Directors — Operations Committee
**Date:** [Monday following Q3 close]
**Re:** Q3 Supplier Failure — Post-Mortem, Financial Impact, and Directive for Supplier Risk Early-Warning System

---

### Purpose

This memorandum summarizes the findings of the post-mortem review following the shutdown of Kyung-Han Precision Components (KHPC), our sole-source supplier of precision-machined motor housings, and establishes a mandatory 90-day initiative to develop a supplier risk early-warning system.

---

### Section 1: Incident Summary

On the second week of the quarter, Kyung-Han Precision Components — a Tier 1 supplier operating from a 200,000-square-foot facility in Southeast Asia — failed a regulatory compliance audit conducted by the regional manufacturing authority. The facility was ordered to cease production pending remediation. KHPC was our sole qualified source for motor housing assemblies used across three product lines.

**Timeline of Impact:**

| Event | Timing |
|-------|--------|
| Compliance audit failure notification received | Day 1 |
| Safety stock exhaustion (11 days of buffer) | Day 12 |
| Production Line A idled | Day 13 |
| Production Line C idled | Day 15 |
| Emergency qualification of alternate supplier initiated | Day 14 |
| First shipment from alternate supplier (air freight, Europe) | Day 22 |
| Full production restored | Day 31 |
| Last contractual penalty notification received | Day 58 |

**Key Observation:** From notification to full restoration, the disruption lasted 31 days. The financial consequences extended well beyond.

---

### Section 2: Financial Impact

The CFO's office has completed the financial impact assessment. Total cost of the KHPC failure:

| Cost Category | Amount |
|---------------|--------|
| Expedited air freight (alternate supplier, 14 shipments) | $4,200,000 |
| Production downtime — Line A (9 days) | $3,100,000 |
| Production downtime — Line C (7 days) | $2,400,000 |
| Contractual delivery penalties (3 customers) | $2,800,000 |
| Lost future contract (customer elected alternate manufacturer) | $1,500,000 |
| **Total** | **$14,000,000** |

For context: $14 million represents approximately 0.44% of annual revenue. The lost future contract alone — a customer we had served for over a decade — represents recurring revenue that will not return.

---

### Section 3: Root Cause Analysis

The post-mortem identified five contributing factors:

1. **Sole-source dependency.** KHPC was the only qualified supplier for motor housings across three product lines. No backup supplier was qualified, and no dual-sourcing strategy was in place for this component category.

2. **Insufficient compliance monitoring.** KHPC's compliance score had been trending downward over the preceding eighteen months, but this trend was not surfaced to procurement leadership. The data existed in the ERP system; it was not being monitored systematically.

3. **Inadequate safety stock.** Eleven days of buffer inventory was insufficient for a component with a 45-day qualification cycle for alternate suppliers.

4. **ERP data gaps.** Supplier performance metrics — including compliance scores, defect rates, and on-time delivery rates — contain missing values for approximately 3% of records, concentrated in fields critical for risk assessment. These gaps reduced the procurement team's ability to detect deteriorating supplier performance.

5. **No predictive risk framework.** Vanguard has no systematic method for identifying suppliers whose risk profiles are deteriorating before a failure event. Risk assessment is reactive, not predictive.

---

### Section 4: Board Directive

The Board's Operations Committee has directed the executive team to develop and deploy a **Supplier Risk Early-Warning System** within 90 days. The system must:

- **Classify** suppliers into risk tiers (Minimal, Low, Moderate, High/Critical) based on observable performance data
- **Predict** total order costs with sufficient accuracy to support procurement budgeting
- **Alert** procurement leadership when a supplier's risk profile is deteriorating — before a failure, not after
- **Be built on data we already have** — one million purchase order records spanning nearly four years in the ERP system

**Accountable Executive:** Marco Reyes, VP of Global Procurement
**Budget Authority:** To be determined following initial data assessment
**Deadline:** 90 days from date of this memorandum
**First Progress Report:** Due to Operations Committee in 30 days

---

### Section 5: Scope of Data Available

The procurement analytics team has identified the following data assets for model development:

| Data Asset | Detail |
|------------|--------|
| Total order records | 1,000,000 |
| Time span | ~4 years |
| Data fields | 22 columns |
| Product categories | Raw Materials, Components, Packaging, Finished Goods |
| Supplier regions | Asia, Europe, North America, South America |
| Shipping methods | Sea, Rail, Road, Air |
| Supplier risk classes | 4 (Minimal, Low, Moderate, High/Critical) |

**Known data quality concerns:**
- ~30,000 records with missing supplier performance metrics (not randomly distributed)
- ~50,000 records with suspected entry errors (implausible lead times, payment terms, stockout frequencies)
- ~2,000 records with extreme values requiring domain review

These quality issues must be addressed as part of the model development process. The board expects an honest assessment of data trustworthiness alongside model results.

---

### Section 6: Expectations

Let me be direct. The KHPC failure was preventable. The warning signs were in our data. We failed to look.

I expect the following from this initiative:

1. **Transparency about data quality.** Do not present model results without first disclosing the limitations of the underlying data. The board will trust an honest assessment far more than an overconfident one.

2. **Actionable output.** A model that lives in a notebook saves no supply chains. The deliverable must include a clear implementation plan for embedding risk scores into procurement workflows.

3. **Ethical clarity.** I am aware that supplier region is likely to be a significant predictor of risk. Before we deploy any model that uses geographic origin as a risk factor, I want a clear analysis of whether we are detecting genuine supply chain risk or encoding historical procurement bias. Our ESG commitments and supplier diversity goals are not negotiable.

4. **Speed.** Ninety days. The next Operations Committee meeting is the deadline.

This is not optional. The board is watching, and our supply chain's integrity depends on getting this right.

---

Diana Cheng
Chief Executive Officer
Vanguard Manufacturing

---

*This exhibit is prepared for case study discussion purposes. All companies, individuals, and scenarios are fictional. Financial figures are illustrative and consistent with the accompanying synthetic dataset.*
