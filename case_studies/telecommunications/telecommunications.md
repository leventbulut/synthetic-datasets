# The Loyalty Tax

**A Data Science Case Study in Subscriber Churn and Retention Analytics**

**From Data to Decisions** | When Keeping Customers Costs More Than Losing Them — Telecommunications Analytics

---

> **Data Resources**
>
> - Dataset: `datasets/telecommunications/synthetic_telecom_20250901.csv`
> - Data Dictionary: `documentation/data_dictionaries/telecom_dictionary.md`
> - Suggested Tasks: `documentation/suggested_tasks/telecom_tasks.md`
> - Exhibit A: CMO Internal Memo — `case_studies/telecommunications/exhibits/exhibit_A.md`
> - Exhibit B: Subscriber Dashboard — `case_studies/telecommunications/exhibits/exhibit_B.md`

---

## I. The Number That Changed Everything

Priya Sharma had been SVP of Customer Retention at Meridian Wireless for four years, through two rounds of network upgrades, a pricing war with a national carrier, and a pandemic that briefly made everyone grateful for any signal at all. She had never seen a quarterly subscriber report like the one sitting on her desk on a Tuesday morning in early March.

Net subscriber growth had turned negative. Not flat — negative. For the first time in the company's eleven-year history, more customers left Meridian in the previous quarter than signed up. The number wasn't catastrophic in isolation — a net loss of roughly 3,200 subscribers out of a base of 550,000 — but it was directional, and in the telecom business, direction is destiny. Once the curve bends downward, it accelerates.

Priya walked the report to the sixth floor, where CMO David Langston was already on his second espresso.

"I've seen it," he said before she could speak. "The board chair called me at seven. He used the words 'structural decline.'"

"It's not structural," Priya said. "Not yet. But the retention spend is out of control." She opened her portfolio. "We spent $4.2 million in retention discounts last quarter. Targeted offers, loyalty credits, plan upgrades at reduced rates. And the churn rate didn't move. It's actually up two basis points."

Langston leaned back. "So we're paying people to stay, and they're leaving anyway."

"Worse than that." Priya set down Exhibit A — the internal memo she had drafted over the weekend. "We're training our loyal customers to act like churners. The discounts are leaking. Subscribers who were never going to leave are calling in, threatening to cancel, because they know we'll offer them $15 off for six months. I ran the numbers: roughly 40% of last quarter's retention credits went to customers who showed zero churn signals in the prior twelve months."

Langston read the memo twice. "The loyalty tax," he said.

"Your phrase. And it's accurate." Priya pulled out the second document. "I want to replace the blanket retention offers with a targeted early warning system. A model that identifies genuine churn risk before the customer calls to cancel — not after."

"What do you need?"

"Access to the full subscriber database. Five hundred fifty thousand records, everything from demographics and plan details to usage patterns, service quality metrics, and billing history. Twenty-two columns. And I need the data science team for eight weeks."

"You'll have the data by end of day," Langston said. "But I need something from you first. The board's Customer Committee meets in six weeks. They want a plan — not a model, a *plan* — for reversing the subscriber loss without doubling the retention budget. Can you deliver that?"

"I can deliver the analysis. Whether the plan is what they want to hear is a different question."

---

## II. Meridian Wireless

Meridian Wireless was a mid-market carrier serving a three-state metropolitan and suburban footprint. With 550,000 active subscribers, the company occupied the precarious middle ground between regional boutique and national giant — large enough to require enterprise-grade infrastructure, small enough that every percentage point of churn hit the income statement visibly.

The subscriber base distributed across four plan tiers: Basic, Standard, Premium, and Enterprise. Basic and Standard plans accounted for the majority of the subscriber population, while Enterprise plans — sold primarily to small businesses and professional offices — commanded the highest average monthly charges but represented a smaller slice of the total base. Contract structures split across month-to-month, one-year, and two-year terms, with month-to-month subscribers comprising the largest single segment (see Exhibit B).

Billing and payment told their own story. Four payment methods were in use — paper check, electronic check, bank transfer, and credit card — and roughly half the base had opted into paperless billing. The payment method distribution was not merely administrative trivia; as Priya's team would soon discover, it carried predictive weight that raised uncomfortable questions.

Usage metrics varied enormously across the subscriber base. Average monthly data consumption centered around 12 GB but ranged from well under a gigabyte for the lightest users to over 100 GB for heavy streamers and remote workers. Voice minutes showed similar dispersion, with a center near 245 minutes and a long right tail stretching past 2,000. Download speeds averaged around 33 Mbps, though network reliability — measured as an uptime ratio — showed a distribution that concerned the engineering team: a center around 0.92 with a non-trivial number of subscribers experiencing reliability below 0.90.

Financially, the mean monthly charge was approximately $45, but the distribution was right-skewed, with Premium and Enterprise plans pulling the tail past $200. The median told a more grounded story of the typical subscriber's monthly outlay.

---

## III. The Data and Its Scars

When the subscriber extract arrived from IT, Priya's lead data scientist, Marcus Chen, spent the first two days simply profiling the file before writing a single line of model code.

"We have a problem," Marcus told the team during the Wednesday standup. "Actually, we have three problems."

The first was structural. Eighteen months earlier, Meridian had migrated its billing system from a legacy platform to a new cloud-based CRM. The migration had been rocky — the VP of Engineering had called it "a root canal without anesthesia" in a company all-hands — and the data bore the scars. Monthly charges and network reliability scores had gaps. Across the 550,000-record extract, approximately 16,500 records — about 3% — showed missing values concentrated in `monthly_charge`, `data_usage_gb`, `network_reliability`, `avg_download_speed`, and `satisfaction_score`. The missingness was not random. It clustered in ways that demanded investigation before any imputation strategy could be trusted.

The second problem was subtler. The old billing system had stored SMS counts in a format that didn't map cleanly to the new platform. During the migration, a batch conversion script had corrupted a subset of SMS records, producing counts that were implausible for any reasonable subscriber behavior. Marcus estimated that roughly 5% of records — about 27,500 — contained entry errors, not just in SMS counts but also in tenure values and customer service call tallies. Tenure figures exceeding 20 years for a company that had existed for eleven were a dead giveaway. Customer service call counts in the dozens per six-month window were physically possible but statistically suspicious.

The third problem lived in the tails. About 1,100 records — roughly 0.2% of the dataset — contained values that were extreme but potentially legitimate: call minutes in the thousands, data usage measured in hundreds of gigabytes, monthly charges that dwarfed the plan rate card. Were these enterprise accounts with unusual usage patterns? Data entry errors that survived validation? Fraudulent accounts? Marcus couldn't tell from the data alone.

"The billing migration explains some of this," said Anita Reeves, the finance analyst embedded with the data science team. "But not all of it. Some of these patterns predate the migration."

"Which means," Marcus said, "we need to characterize what's broken before we build anything on top of it."

---

## IV. Two Predictions, Two Stakes

By the second week of the engagement, the team had mapped the analytical work into two parallel tracks.

**Track One: The Early Warning System.** The business question was deceptively simple: *which subscribers are going to leave, and can we identify them before they call to cancel?* The target variable was `churn_prediction`, a three-class label — Retain, At Risk, and Likely Churn. Priya needed a model that could stratify the entire subscriber base so her retention team could focus their limited budget on the customers most likely to leave and most worth saving.

Marcus framed the modeling challenge for the team. "The class distribution matters here. We have three categories, and they're not evenly split. A model that defaults to the majority class will look decent on overall accuracy but will be useless for the business. We need to decide what's worse — missing a subscriber who's about to churn, or wasting a retention offer on someone who was never leaving."

Priya didn't hesitate. "Missing a churner costs us the lifetime value of that subscriber — which for a Standard plan customer on a two-year contract is north of $1,000. A wasted retention offer costs us $50 in discount credits. The math isn't even close."

"Except," Marcus said, "that $50 adds up fast when you multiply it by tens of thousands of false positives. That's exactly how we got to $4.2 million in retention spend last quarter."

**Track Two: The Satisfaction Gap.** The second model targeted `satisfaction_score`, a continuous variable on a 1-to-10 scale with a center around 5.5. Satisfaction surveys were the company's primary instrument for gauging customer sentiment, but only about 30% of subscribers completed them in any given quarter. That left Meridian flying blind on the mood of 385,000 customers.

"If we can predict satisfaction from usage patterns and service quality metrics," Priya said, "we don't have to wait for a survey that most people ignore. We can estimate satisfaction in real time and intervene before dissatisfaction turns into a cancellation call."

Langston was enthusiastic about this track. "The customer experience team has been begging for a satisfaction proxy for two years. If you can build one that's credible, I'll fund the integration into the CRM myself."

But Marcus flagged a concern that the executives hadn't considered. "Satisfaction and churn are related, but they're not the same thing. We'll almost certainly find subscribers who are dissatisfied but stay — because they're locked into contracts, or because switching costs are high — and subscribers who are perfectly satisfied but leave anyway for a better price. The model needs to capture the *drivers* of satisfaction independently from churn, or we'll end up with a prediction that's just a mirror of the churn model with a different label."

---

## V. The Proxy Problem

It was during the fourth week that the project hit an ethical wall.

Marcus had been running feature importance analyses across both models, and one finding kept surfacing with uncomfortable consistency. Two variables — `contract_type` and `payment_method` — were among the strongest predictors of churn. Month-to-month subscribers churned at dramatically higher rates than those on annual or two-year contracts, which was expected and mechanically obvious. But the payment method signal was harder to dismiss. Subscribers who paid by paper check showed significantly elevated churn risk compared to those using credit cards or bank transfers, even after controlling for plan type, tenure, and usage patterns.

Marcus brought the finding to Priya on a Friday afternoon.

"On the surface, this is just a useful feature," he said. "Paper check customers churn more. If we include it in the model, prediction improves. But I looked at the demographics." He pulled up a cross-tabulation. "Paper check payment is heavily concentrated among older subscribers. The correlation with age is strong. The subscribers who don't use paperless billing, who pay by check, who are on month-to-month contracts — they skew significantly older and, based on usage patterns, less digitally engaged."

Priya saw where this was going. "So if we target month-to-month paper-check customers with aggressive retention offers..."

"We're effectively targeting elderly and digitally underserved subscribers. We're profiling people based on proxies for age and digital literacy." Marcus paused. "And the timing is terrible. AARP filed a complaint last month against TelcoNorth for exactly this — using contract type and payment method to segment customers for differential pricing. They called it 'age discrimination by algorithm.'"

Priya stared at the cross-tabulation for a long time. The ethical dilemma was genuine and it cut both directions.

On one side: the model was identifying real churn risk. Older subscribers on month-to-month plans who pay by check *do* leave at higher rates. Ignoring that signal meant missing genuinely at-risk customers who might benefit from outreach — a proactive call, a simplified billing option, a plan review. Failing to act on the data could mean *worse* outcomes for these subscribers, who might churn into inferior service with a competitor or lose coverage altogether.

On the other side: acting on the signal meant treating subscribers differently based on characteristics that served as proxies for protected attributes. An aggressive retention campaign targeting this segment would look, to a regulator or advocacy group, indistinguishable from age-based profiling. And the "help" being offered — discounts, plan changes, digital migration incentives — might not be help at all. It might be patronizing, presumptuous, or coercive.

"There's a third angle," Anita added from the corner of the room. "If we *exclude* contract type and payment method and the model gets worse, we'll miss churn signals that happen to correlate with age. Is that more ethical? We'd be protecting a demographic by letting them churn in silence."

Marcus nodded slowly. "And there's a fourth angle. If we include the features but don't adjust the retention approach, we'll send the same aggressive discount offers to this segment that we send to everyone — offers designed for digitally savvy 30-year-olds. A 72-year-old on a Basic plan who pays by check might get an email with a QR code for a loyalty discount she can't redeem."

Priya didn't resolve the question that afternoon. She suspected there wasn't a clean resolution — only trade-offs that needed to be made transparently and documented explicitly.

---

## VI. Six Weeks

The board's Customer Committee meeting was five weeks away. Priya met with Langston and CFO Renata Oliveira to structure the presentation.

"Three sections," Priya said. "First: what the data actually tells us, including what it *can't* tell us. The board needs to understand that a model built on migrated data with known gaps has limits. Confidence in the outputs depends on confidence in the inputs."

"Keep the data quality section short," Langston said. "They'll lose the room."

"I'll keep it efficient, but I won't skip it. If we deploy a churn model that's built on corrupted SMS data and missing billing records, and it produces bad recommendations, I want the board to understand why — and I want the record to show that I flagged the risk."

Langston conceded the point.

"Second section: the models themselves. What drives churn, what drives satisfaction, and where those drivers overlap and diverge. I want to show the board that dissatisfaction and churn are related but not identical — that fixing satisfaction doesn't automatically fix retention, and that some of our most at-risk subscribers aren't unhappy. They're just not locked in."

"And the third section?"

Priya set the AARP complaint printout on the table. "The proxy problem. We can build a model that identifies churn risk with useful precision. But if the retention team acts on it naively — if we target month-to-month paper-check subscribers with the same playbook we use for everyone else — we will face a discrimination complaint within eighteen months. The board needs to decide: how do we want to use this model, and what safeguards do we put around it?"

Renata looked at the numbers. "The $4.2 million in retention spend last quarter — that's a run rate of nearly $17 million a year. If the model can cut even 30% of the wasted spend and redirect it to genuinely at-risk subscribers, the ROI case writes itself."

"The ROI case is the easy part," Priya said. "The hard part is convincing the board that *how* we target matters as much as *who* we target."

---

## Your Assignment

You have been engaged as an external analytics consultant supporting Priya Sharma's retention initiative at Meridian Wireless. Using the company's 550,000-subscriber dataset, you will work through four phases — mirroring the arc of a real-world churn analytics engagement: from data audit to boardroom presentation. The companion task set provides additional analytical questions that extend the work begun here.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Meridian's dataset carries the scars of an eighteen-month billing system migration. Corrupted SMS records, missing billing fields, and implausible tenure values have left marks that no algorithm can paper over. Your first task is to determine how deep those marks go.

**Guiding questions:**
- Where are the data quality issues concentrated — in specific plan types, contract segments, or subscriber demographics? Does the pattern of missingness align with the billing migration narrative, or does it suggest additional undocumented problems?
- Under what circumstances would you impute missing values versus exclude records? How do your choices affect downstream predictions — particularly for the subscriber segments where missingness is concentrated?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, corrupted fields, entry errors, and distributional anomalies. For each issue, state what you found, quantify its scope, and recommend a handling strategy. This report should answer Marcus Chen's foundational question: *Is the data trustworthy enough to build retention models on?*

---

### Phase 2: The Prediction Challenge

Meridian's churn rate is climbing, retention spend is spiraling, and the board wants answers.

#### Part A — Churn Risk Classification

The retention team has a limited budget and cannot offer discounts to all 550,000 subscribers. Predict `churn_prediction` (Retain / At Risk / Likely Churn).

**Guiding questions:**
- Given the three-class target, what metric should you optimize — and why? What is the relative cost of a false negative (missing a subscriber about to churn) versus a false positive (wasting a retention offer on a loyal customer)?
- Identify the top features driving churn risk. Which are actionable (Meridian can intervene) and which are structural (useful for stratification but not directly modifiable)?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with business-appropriate metrics, and interpretation. Address the class distribution and the asymmetric cost of misclassification explicitly. Conclude with a clear recommendation: which subscriber signals should the retention team monitor, and how would you embed this model into the CRM workflow?

#### Part B — Satisfaction Score Regression

Only 30% of subscribers complete satisfaction surveys. The customer experience team needs a proxy. Predict `satisfaction_score`.

**Guiding questions:**
- Satisfaction centers around 5.5 on a 1–10 scale. Investigate the tails of the distribution. What subscriber profiles are associated with extreme dissatisfaction? With unexpectedly high satisfaction despite poor service metrics?
- How should Meridian use satisfaction predictions operationally? Where should the customer experience team trust the model, and where should they verify with direct outreach?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis, preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to CMO David Langston: how should predicted satisfaction scores inform the customer experience strategy? Characterize the error distribution — where does the model perform well, and where does it break down?

---

### Phase 3: The Ethical Crossroads

Marcus Chen's analysis revealed that `contract_type` and `payment_method` are strong predictors of churn — but they are proxies for age and digital literacy. The AARP complaint against TelcoNorth looms in the background.

**Guiding questions:**
- Should the churn model include `contract_type` and `payment_method` as predictors? Construct arguments for both positions. What alternative approaches might capture the predictive signal without creating a de facto demographic profiling tool?
- If Meridian deploys a churn risk score in its CRM, what safeguards should be in place to prevent retention campaigns from disproportionately targeting — or neglecting — elderly and digitally underserved subscribers?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on the proxy variable question. Defend your position with both analytical evidence from the data and ethical reasoning. Address the counterargument directly. If you propose an alternative approach (e.g., separate models by segment, fairness-adjusted thresholds, human-in-the-loop review for flagged demographics), specify exactly how it would work and what trade-offs it introduces.

---

### Phase 4: The Board Room

It is mid-April. Priya Sharma stands before Meridian's Customer Committee. The $4.2 million retention spend is the burning platform.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the CMO, the CFO, two independent board members, and the VP of Customer Experience. Communicate: (a) the scope of the churn problem and what's driving it, (b) what your models reveal about which subscribers are most at risk and what drives satisfaction, (c) your recommended retention strategy with projected savings and subscriber impact, and (d) the data limitations, model uncertainties, and ethical guardrails the board should understand. Renata Oliveira will ask: *"If we cut the retention budget by half and target it better, do we get more subscribers to stay?"* Be ready.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in Meridian's data that is not covered by Phases 1–3? A segment that defies the churn model's assumptions, a usage pattern that predicts satisfaction better than any survey, an interaction between service quality and contract type that the engineering team should investigate, or a billing anomaly that the migration didn't fully explain. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

| Resource | Path |
|---|---|
| Dataset | `datasets/telecommunications/synthetic_telecom_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/telecom_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/telecom_tasks.md` |

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Loyalty Tax." *From Data to Decisions*, Case 8. University of North Texas.
