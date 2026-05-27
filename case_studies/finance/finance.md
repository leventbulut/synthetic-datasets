# The Model That Cried Safe

**A Data Science Case Study in Credit Risk and Fair Lending**

---

**From Data to Decisions** | When the Model Says "Fine" but the Charge-Offs Say Otherwise — Finance Analytics

---

## I. The Number That Didn't Match

On a Monday morning in early March, Sarah Koh arrived at the twelfth-floor executive suite of Atlas National Bank to find two documents waiting in her inbox. The first was the monthly charge-off report from the consumer lending division: losses had jumped to 3.8% of the outstanding portfolio in the most recent quarter, up from 2.6% the quarter before and nearly double the 2.1% rate the bank's internal credit risk model had predicted. The second was a calendar invitation from the Office of the Comptroller of the Currency — the OCC examiner assigned to Atlas's annual stress test wanted to schedule a preliminary review for the first week of April.

Sarah had been Chief Risk Officer at Atlas National for four years. The bank — a mid-size regional institution with $28 billion in assets, three hundred branches across five regions, and a consumer loan portfolio that had grown aggressively since a merger eighteen months earlier — occupied an uncomfortable middle ground in the regulatory landscape. Too large to fly under the radar. Too small to absorb the kind of loss acceleration the charge-off report was describing. And too dependent on a credit risk model that was, by every measurable indication, lying.

The model had been built five years ago by a team of quantitative analysts who had since moved on to larger institutions. It had been trained on a fraction of the current portfolio — roughly 180,000 accounts drawn primarily from the bank's pre-merger footprint in the Northeast. Since then, Atlas had absorbed Lakeview Savings, a community bank concentrated in the Southeast and Midwest, and expanded its credit card and personal loan products into the Southwest and West. The customer base had quadrupled. The model hadn't been retrained.

"It's not that the model is wrong," said Daniel Reeves, Sarah's analytics lead, when she called him at seven-thirty that morning. "It's that it's answering a question about a bank that doesn't exist anymore."

## II. Seven Hundred Fifty Thousand Stories

By the following week, Sarah had authorized a full data pull from the bank's enterprise data warehouse. The result was a dataset of 750,000 customer records spanning 23 columns — every active consumer account in Atlas National's portfolio, drawn from both the original Atlas core banking platform and the legacy Lakeview system that had been migrated during the merger integration.

The 23 columns captured a broad landscape. Demographic attributes included age (mean of approximately 44 years across the customer base), income (median of roughly $36,315, though the mean was pulled higher by a long right tail of affluent customers), and education level ranging from high school through doctoral degrees. Credit behavior metrics tracked credit scores (mean around 680, spanning the full 300-to-850 range), credit utilization ratios, debt-to-income ratios, and the number of credit cards per customer. Account history captured employment years, late payment months, and monthly spending. A regional field tagged each customer to one of five geographies: Northeast (20%), Southeast (25%), Midwest (20%), Southwest (15%), and West (20%) — a distribution that still reflected Lakeview's southern footprint.

Two columns anchored the analytical challenge ahead.

The first was `credit_risk`, a four-level classification — Very Low, Low, Medium, and High — that the legacy model had assigned to every account. This was the variable that the OCC examiner would scrutinize. If Atlas couldn't demonstrate that its risk classifications were accurate, defensible, and free from discriminatory bias, the consequences ranged from mandatory remediation to a formal enforcement action.

The second was `fraud_risk_score`, a continuous variable that the compliance team used to prioritize manual account reviews. The score was clipped between 0.01 and 12.0, but the typical range clustered between 0.19 and 1.0, with a pronounced rightward skew — most accounts scored low, while a small number generated the outsized scores that triggered investigation. The problem was volume: the compliance team was drowning in false positives, reviewing hundreds of low-risk accounts for every genuine fraud case, because the scoring thresholds had never been calibrated against outcomes.

Daniel's team began their audit with a warning that landed like a stone. "The Lakeview migration was rough," he told Sarah during a working session. "Two legacy core banking platforms, different field definitions, different validation rules. We've got gaps. Unemployed customers are systematically missing income data — the Lakeview system didn't require it for certain loan products. And the credit card portfolio that came over from the old Atlas platform has entry errors in fields like employment years and number of credit cards that predate the merger. Some of these records say customers have been employed for seventy years or hold forty credit cards. Nobody caught it because nobody was looking."

The scope of the data quality issues became clearer as the team dug in. Across the 750,000 records and 23 columns, approximately 22,500 records — about 3% — carried missing values concentrated in income, investment value, savings rate, credit utilization, debt-to-income ratio, and monthly spending. The missingness wasn't random. It tracked employment status: unemployed customers were far more likely to have incomplete financial profiles, creating a systematic gap that any model trained on the raw data would inherit. Beyond the missing values, roughly 37,500 records — 5% of the portfolio — contained entry errors: employment years stretching to 55, 70, even 100 years; customers apparently holding 25 to 60 credit cards; late payment histories spanning 40 to 100 months. And then there were the outliers — approximately 1,500 records, just 0.2% of the total, with incomes between $1 million and $5 million, credit scores in the 30-to-150 range, or monthly spending between $80,000 and $250,000. Real? Possible. But suspiciously concentrated in accounts that had been migrated from the older Atlas platform.

"The question," Daniel said, "is whether we can build something defensible on top of this. The OCC isn't going to accept 'the data was messy' as an excuse."

## III. The Variables That Worked Too Well

By the third week, Sarah's team had moved from diagnosis to modeling. The classification challenge — predicting `credit_risk` across four levels — demanded a model that could withstand regulatory scrutiny. The regression challenge — estimating `fraud_risk_score` to help the compliance team triage its review queue — demanded a model that could reduce false positives without letting genuine fraud slip through.

Early results were promising. The classification models achieved reasonable separation across the four risk categories, and the regression models captured the right-skewed distribution of fraud scores with acceptable accuracy. But a discovery during feature importance analysis brought the project to a confrontation that Sarah had been dreading.

Two variables — `employment_status` and `home_ownership` — consistently appeared among the strongest predictors in both models. The signal was clean, interpretable, and statistically robust. From a pure prediction standpoint, they were exactly the kind of features a risk modeler wanted: stable, available at origination, and correlated with the targets in economically intuitive ways.

Rachel Osei, head of the Fair Lending compliance unit, was the one who raised the alarm. She appeared in Sarah's office on a Thursday afternoon with a folder of disparate impact analyses. "Employment status and home ownership are proxies," she said. "They correlate with race, ethnicity, and national origin in ways that are well-documented in the fair lending literature. If you build a model that relies on these features, and that model produces systematically different outcomes for protected classes, you've got a disparate impact problem. It doesn't matter that the variables aren't themselves protected. The effect is what matters."

Sarah understood the argument. She also understood the counter-argument. Atlas's portfolio was genuinely riskier among customers with unstable employment or without home equity — not because of who those customers were, but because of the financial fragility those conditions created. Removing the variables would make the model less accurate. A less accurate model would misclassify risk, potentially in both directions — flagging safe borrowers for enhanced scrutiny while missing genuinely risky ones. The OCC examiner would notice the performance gap. So would the charge-off report.

"You're asking me to choose between a model the regulators will challenge for bias and a model they'll challenge for inaccuracy," Sarah said.

Rachel didn't blink. "I'm asking you to understand that they might challenge it either way."

## IV. Two Audiences, One Week

The calendar compressed everything. On Tuesday, Sarah would present to the Board Risk Committee — seven directors who controlled the bank's risk appetite and capital allocation. On Friday, the OCC examiner would arrive for the preliminary stress test review.

The board wanted assurance. Were the rising charge-offs a temporary blip or a structural problem? Was the credit risk model reliable? Did the bank have adequate reserves? They would ask questions in plain language and expect answers without jargon.

The examiner wanted evidence. Were the risk classifications statistically valid? Had the model been tested for disparate impact? Were data quality issues documented and addressed? The examiner would ask questions in regulatory language and expect answers with full technical documentation.

Sarah stood at the intersection of two conversations — one about business judgment, one about regulatory compliance — knowing that a misstep in either room could cascade. A model that satisfied the board's appetite for simplicity might fail the examiner's demand for rigor. A model that satisfied the examiner's demand for fairness might fail the board's demand for accuracy. And somewhere in the data — 750,000 records, 23 columns, 22,500 missing values, 37,500 entry errors, and two variables that worked too well — lay the answers that both audiences needed but neither might want to hear.

She opened her laptop, pulled up the dataset, and began to build the case.

---

## Your Assignment

You have been brought in as an external data science consultant engaged by Atlas National Bank's Risk Analytics group. Using the bank's 750,000-record consumer lending dataset, you will work through four phases — mirroring the real-world arc of a regulatory-grade analytics engagement: from raw data to boardroom and examiner presentation.

The companion task set (`documentation/suggested_tasks/finance_tasks.md`) provides structured analytical exercises aligned with this case. The phases below frame those tasks within the narrative and ethical context that a working data scientist at Atlas would face.

---

### Phase 1: Discovery & Diagnosis

Before any model can be defended to a regulator, the data must be understood.

Sarah's team knows the dataset carries the scars of a two-platform merger. Your first task is to determine how deep those scars go — and whether the data is trustworthy enough to build on.

**Guiding questions:**
- The dataset contains approximately 22,500 records with missing values (~3% of the portfolio), concentrated in financial fields for unemployed customers and in credit behavior fields for others. Is this missingness random, or does it follow a pattern tied to employment status or other customer attributes? What are the implications for any downstream model?
- Beyond missing values, the team has flagged entry errors in employment years, number of credit cards, and late payment months, as well as outliers in income, credit scores, and monthly spending. Design an EDA plan that would surface the full scope of these issues before model training begins.
- The median income is approximately $36,315, yet the dataset spans from $22,000 to well beyond $500,000. What does this shape reveal about the portfolio composition, and how might extreme values affect model performance?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). For each issue you discover, state what you found, assess its likely cause (merger artifact, system migration, or genuine population variation), quantify its scope, and recommend a handling strategy (impute, cap, flag, remove, or leave as-is). Justify your choices. This report must be defensible to both internal stakeholders and a regulatory examiner.

---

### Phase 2: The Prediction Challenge

Sarah has two mandates, one dataset, and three weeks before the OCC examiner arrives.

#### Part A — Credit Risk Classification

The OCC will evaluate whether Atlas's risk classifications are accurate and unbiased. Predict `credit_risk` (Very Low / Low / Medium / High — four classes).

**Guiding questions:**
- The credit risk variable has four levels. Examine the class distribution in the data. How would you handle any imbalance, and what evaluation metrics are most appropriate when the regulatory cost of misclassifying a High-risk borrower as Low exceeds the cost of the reverse error?
- Credit scores average around 680, but the range spans 300 to 850, with suspected outliers in the 30-to-150 range. How would you handle these suspect values — are they data errors, or could they represent legitimate edge cases?
- Design a feature engineering strategy. Which raw columns might benefit from transformation, interaction terms, or binning? How would you validate that engineered features improve performance without introducing data leakage?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, training of at least two distinct algorithms, evaluation with business-appropriate metrics, and interpretation. Address any class imbalance explicitly. Conclude with a plain-language summary: which borrowers are most likely to be misclassified by the current system, and what signals should Atlas's risk team watch for?

#### Part B — Fraud Risk Score Regression

The compliance team is drowning in false positives. Predict `fraud_risk_score` (continuous).

**Guiding questions:**
- The fraud risk score is clipped between 0.01 and 12.0, but most values cluster between 0.19 and 1.0 with a pronounced right skew. What regression approaches would you consider, and should the target variable be transformed? How would you handle the boundary effects created by clipping?
- How would you translate regression predictions into an actionable triage system? What threshold would separate accounts requiring manual review from those that can be auto-cleared, and how would you communicate the trade-off between review volume and missed fraud to the compliance team?
- The fraud risk score distribution has a long right tail. Should you train a single model across the full range, or consider separate approaches for the bulk of the distribution versus the extreme scores?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (distribution shape, boundary effects, skewness), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to the compliance team: how should the predicted scores be used to prioritize account reviews? Where is the model most and least reliable?

---

### Phase 3: The Ethical Crossroads

Rachel Osei's analysis shows that `employment_status` and `home_ownership` are proxies for protected characteristics. The model performs best with them. The Fair Lending team says they create disparate impact risk. Sarah must decide.

**Guiding questions:**
- If employment status and home ownership improve model accuracy but produce systematically different risk classifications across demographic groups, how would you assess whether the model's predictions constitute disparate impact? What specific fairness metrics would you compute, and what thresholds would you apply?
- Sarah frames the dilemma: "a model the regulators will challenge for bias versus a model they'll challenge for inaccuracy." Construct arguments for both positions. Is there a middle path — perhaps a constrained model, post-hoc adjustments, or a dual-model approach — that balances predictive power with fair lending obligations?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position: Should Atlas National include employment status and home ownership as features in its credit risk model? Defend your position with both analytical evidence from the data and legal/ethical reasoning grounded in fair lending principles. If you propose a middle path, specify exactly how it would work in practice — vague compromises will not be accepted.

---

### Phase 4: The Board Room

It is the first week of April. On Tuesday, Sarah faces the Board Risk Committee. On Friday, the OCC examiner arrives.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the Board Risk Committee (non-technical directors) and, separately, a regulatory examiner (deeply technical). Prepare a single document that serves both: communicate (a) the scale of the model accuracy problem and its financial exposure, (b) what your models reveal about which borrowers are mispriced by the legacy system, (c) your recommended path to a defensible model, and (d) what the data *cannot* tell them. No jargon for the board. Full methodological transparency for the examiner. The best executive briefs accomplish both.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best risk analysts don't just answer the questions they're given — they find the questions nobody thought to ask. What did you discover in the data that is not covered by Phases 1–3? A regional concentration of risk that the legacy model missed? A customer segment where fraud scores and credit risk diverge unexpectedly? A data pattern that suggests the Lakeview migration introduced systematic bias? An opportunity to reduce the compliance team's workload by 40% with a simple threshold adjustment? There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

## Data Resources

| Resource | Path |
|---|---|
| Customer Dataset | `datasets/finance/synthetic_finance_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/finance_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/finance_tasks.md` |

Students should begin by loading the dataset and performing independent exploratory data analysis before engaging with the discussion questions. The data dictionary provides complete column definitions, data types, and valid value ranges.

---

## Exhibits

- **[Exhibit A](exhibits/exhibit_A.md)** — Internal memorandum from Chief Credit Officer Marcus Webb to Sarah Koh regarding stress test preparation and legacy model performance
- **[Exhibit B](exhibits/exhibit_B.md)** — Atlas National Bank Risk Dashboard — Portfolio Composition Snapshot

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Model That Cried Safe." *From Data to Decisions*, Case 4. University of North Texas.
