# Exhibit A — Internal Memorandum

---

**ATLAS NATIONAL BANK**
*Office of the Chief Credit Officer*

---

**FROM:** Marcus Webb, Chief Credit Officer
**TO:** Sarah Koh, Chief Risk Officer
**CC:** Daniel Reeves (SVP, Risk Analytics); Rachel Osei (Director, Fair Lending Compliance)
**DATE:** March 3
**SUBJECT:** Stress Test Preparation — Legacy Model Performance and Data Integrity Concerns

---

Sarah,

I'm writing ahead of our Wednesday steering committee to lay out what I'm seeing on the credit side. The numbers are worse than the quarterly summary suggests, and I want you to have the full picture before we scope the OCC engagement.

**Model vs. Reality — The Divergence Is Accelerating**

Our internal credit risk model predicted a 2.1% default rate for Q3. Actual charge-offs came in at 3.8%. That's an 81% miss, and it's not an outlier — the model underpredicted in each of the previous three quarters, with the gap widening each time:

| Quarter | Model Predicted Default Rate | Actual Charge-Off Rate | Variance |
|---|---|---|---|
| Q4 (Two Years Prior) | 1.9% | 2.0% | +0.1 pp |
| Q1 (Prior Year) | 2.0% | 2.3% | +0.3 pp |
| Q2 (Prior Year) | 2.0% | 2.6% | +0.6 pp |
| Q3 (Prior Year) | 2.1% | 3.8% | +1.7 pp |

The trend is clear: the model is systematically underestimating risk, and the error is growing. At current trajectory, we're looking at a potential 4.5–5.0% charge-off rate by year-end if the underlying drivers aren't addressed.

**Why the Model Is Failing**

The model was built five years ago on approximately 180,000 accounts — all from the legacy Atlas footprint, predominantly Northeast geography. Since then:

1. **The Lakeview merger** added roughly 300,000 consumer accounts concentrated in the Southeast and Midwest, with different product mix, underwriting standards, and risk profiles. The model has never been recalibrated to reflect this population.
2. **Product expansion** into unsecured personal loans and balance transfer credit cards introduced risk characteristics the original model wasn't designed to capture.
3. **The macroeconomic environment** has shifted. Unemployment patterns, interest rate sensitivity, and consumer savings behavior bear little resemblance to the training period.

In short, we're navigating a $28 billion institution with a compass calibrated for a different ocean.

**Portfolio Composition — What the Data Shows**

I pulled a full snapshot from the data warehouse — 750,000 active customer records across 23 data fields. A few headline numbers:

- **Credit score distribution:** Mean ~680, but the range extends from 300 to 850. The post-merger portfolio has a heavier tail below 600 than the model was trained on.
- **Income profile:** Median income of approximately $36,315, but the distribution is heavily right-skewed. We have a meaningful cluster of high-net-worth clients (income above $200K) alongside a large base of moderate-income borrowers. The model treats income linearly — it shouldn't.
- **Regional exposure:** The Southeast now represents 25% of the portfolio (up from 8% pre-merger). The Midwest is at 20%. These regions have different default dynamics than the Northeast, and the model has no regional adjustment.
- **Employment mix:** Roughly 30% of the portfolio is full-time employed, but we have material exposure across part-time, self-employed, retired, and unemployed segments. Default rates vary substantially across these groups — a signal the model currently ignores.

**Data Quality — The Merger Left Scars**

Daniel Reeves's team has flagged significant data quality issues stemming from the platform migration:

- **Missing values:** Approximately 22,500 records (~3%) have gaps, concentrated in income, investment value, and savings rate fields. The missingness appears systematic — unemployed customers are disproportionately affected, likely because the Lakeview system didn't require income documentation for certain secured products.
- **Entry errors:** Roughly 37,500 records (~5%) contain implausible values — employment tenures exceeding 55 years, customers reportedly holding 25+ credit cards, late payment histories spanning 40–100 months. These appear to be legacy data entry artifacts that were never cleaned.
- **Outliers:** About 1,500 records (~0.2%) show extreme values — incomes between $1M and $5M, credit scores below 150, monthly spending above $80K. Some may be legitimate high-net-worth accounts; others are almost certainly errors.

Any model we present to the OCC must account for these issues transparently. The examiner will ask.

**My Recommendation**

We need to rebuild the credit risk model from the ground up, using the full 750,000-record dataset. The current four-class system (Very Low / Low / Medium / High) is the right framework — the OCC is familiar with it, and our capital adequacy calculations depend on it. But the underlying model must reflect the bank we are today, not the bank we were five years ago.

I'm also recommending that we engage your Fair Lending team early. Daniel's preliminary feature analysis shows that employment status and home ownership are strong predictors — but Rachel will want to evaluate those for disparate impact before we commit to a model architecture. Better to have that conversation now than in the examiner's conference room.

We have approximately four weeks before the OCC preliminary review. That's tight but feasible if we start this week.

Let's discuss Wednesday.

— Marcus

---

*This exhibit is a fictional internal communication prepared for case discussion. All statistics referenced are consistent with the case dataset available at `datasets/finance/synthetic_finance_20250901.csv`. Students should verify cited figures against the raw data.*
