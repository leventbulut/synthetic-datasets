# The Weakest Link

**A Data Science Case Study in Supply Chain Risk and Cost Prediction**

**From Data to Decisions** | A $14M Supplier Failure and the Race to Build an Early-Warning System — Supply Chain Analytics

---

> **Data Resources**
>
> - Dataset: `datasets/supply_chain/synthetic_supplychain_20250901.csv`
> - Data Dictionary: `documentation/data_dictionaries/supply_chain_dictionary.md`
> - Suggested Tasks: `documentation/suggested_tasks/supplychain_tasks.md`
> - Exhibit A: CEO Memo — `case_studies/supply_chain/exhibits/exhibit_A.md`
> - Exhibit B: Global Procurement Dashboard — `case_studies/supply_chain/exhibits/exhibit_B.md`

---

## I. The Phone Call

Marco Reyes was twelve minutes into his Tuesday morning staff meeting when his phone vibrated with a message from the CEO's executive assistant: *Board call in 30 minutes. Your attendance is mandatory.* He excused himself, walked to his office on the seventh floor of Vanguard Manufacturing's headquarters, and closed the door.

He already knew what the call was about. Three weeks earlier, Vanguard's sole-source supplier of precision-machined motor housings — a components manufacturer operating out of a sprawling industrial park in Southeast Asia — had failed a regulatory compliance audit. The facility was shut down pending remediation. No timeline for reopening. No alternative supplier qualified for the specification. No inventory buffer beyond eleven days of safety stock.

What followed was the most expensive quarter in Vanguard Manufacturing's procurement history. Expedited air freight from a hastily qualified backup supplier in Europe. Two production lines idled for nine days while engineering validated the substitute parts. Three contractual delivery commitments missed, triggering penalty clauses with downstream customers. By the time the dust settled, the CFO's office had tallied the damage: $14 million in expedited shipping, production downtime, contractual penalties, and lost future contracts.

On the board call, the message was blunt. The CEO, Diana Cheng, told the executive team that the board's Operations Committee wanted a supplier risk early-warning system — not a strategy deck, not a consulting engagement, but a working analytical model — within ninety days. She looked at Marco through the camera. "You own this, Marco. What do you need?"

"Data," he said. "And about a week to figure out how bad the problem actually is."

---

## II. Vanguard Manufacturing

Vanguard Manufacturing was a diversified industrial company with $3.2 billion in annual revenue, producing everything from precision components for aerospace customers to packaging materials for consumer goods clients. Its global procurement operation sourced raw materials, components, packaging, and finished goods from suppliers spanning four continents — Asia, Europe, North America, and South America — using a mix of sea, rail, road, and air freight (see Exhibit B).

Marco's procurement team pulled one million purchase order records from Vanguard's ERP system, covering nearly four years of transactions across 22 data fields. The extract captured order details — quantities, unit prices, lead times, priorities — alongside supplier performance metrics such as on-time delivery rates, defect rates, compliance scores, and composite supplier ratings. Logistics and inventory data rounded out the picture: shipping methods and costs, warehouse utilization, inventory turnover, stockout frequency, and payment terms.

The numbers painted a sprawling operation. Order quantities ranged from 10 units to 50,000, with a median of roughly 665 units per order. Unit prices spanned from $1 for commodity fasteners to $500 for specialized subassemblies, with a median of approximately $12.18. Total order costs followed a log-normal distribution centered near $1,808, though the typical range stretched from $2,000 to $15,000, with the distribution clipped at $100 on the low end and $500,000 at the high end.

Lead times varied from next-day delivery on domestic road shipments to 90-day ocean transits from Asia. The median was 12 days — a number that concealed enormous variation across shipping methods and supplier regions. Order priorities were classified into four tiers — Low, Medium, High, and Critical — reflecting the downstream impact of a delayed or defective shipment.

"A million records across four years," said Lena Park, Marco's director of procurement analytics. "That should be enough to build something useful."

"Should be," Marco agreed. "But I want to know what the data actually looks like before we promise the board anything."

---

## III. The ERP Problem

Vanguard's ERP system had not been implemented all at once. The North American operations had gone live first, followed by Europe eighteen months later, then Asia and South America in a staggered rollout that had taken the better part of two years. Each regional implementation team had made slightly different choices about data capture, field definitions, and validation rules. The result was a dataset that looked unified in structure but carried the fingerprints of its fragmented origins.

Lena's team discovered the scars quickly. Supplier performance metrics — the ratings, defect rates, on-time delivery rates, compliance scores, and return rates that Marco needed most for a risk model — had gaps. Approximately 30,000 records, roughly 3% of the dataset, were missing values in these fields. The missingness was not random; it followed patterns that Lena suspected were tied to regional ERP rollout timelines and data entry practices.

"The fields that matter most for risk assessment are the ones with the most holes," she told Marco. "If we ignore the missing data, we lose 30,000 records. If we impute it carelessly, we might be filling in fiction."

There were other problems. About 2,000 records — a fraction of a percent — contained values that were technically possible but operationally implausible: order quantities in the hundreds of thousands, unit prices in the thousands of dollars for commodity items, shipping costs that exceeded the value of the goods. These were genuine outliers, or they were data entry errors. Distinguishing between the two required domain knowledge that no algorithm could provide on its own.

More troubling were the entry errors that Lena's team flagged in roughly 50,000 records — 5% of the dataset. Lead times stretching to 400 days. Payment terms of 500 days. Stockout frequencies that would imply a warehouse running empty every few days. These were not edge cases or unusual business arrangements; they were mistakes, likely introduced during the chaotic early months of regional ERP rollouts when procurement staff were learning new systems under production pressure.

"So our data has three layers of problems," Marco summarized. "Missing values that aren't random. Outliers that might be real or might be errors. And entry mistakes that are definitely wrong but mixed in with legitimate records."

Lena nodded. "Welcome to enterprise data."

---

## IV. Two Models, Two Questions

Despite the data quality challenges, the board's mandate was clear: build an early-warning system. Marco and Lena structured the work into two parallel tracks.

**Track One: Supplier Risk Classification.** The ERP system already classified suppliers into four risk tiers — Minimal (0), Low (1), Moderate (2), and High/Critical (3). The distribution was striking: the High/Critical tier was by far the most populated, comprising roughly 55–60% of all records. Minimal-risk suppliers accounted for the smallest share. This was not a balanced classification problem.

"Most of our orders are flowing through suppliers the system considers high-risk," Lena observed. "Either we have a genuinely risky supply base, or the risk scoring methodology is too aggressive. Either way, the board needs to understand this distribution before they act on model predictions."

The goal was to build a vendor pre-qualification model that could score new or existing suppliers based on observable attributes — performance history, compliance metrics, regional factors, order patterns — and flag those most likely to fall into the Moderate or High/Critical tiers before a catastrophic failure occurred. The asymmetry of misclassification costs was stark: classifying a High/Critical supplier as Minimal risk could lead to another $14 million incident. Classifying a Minimal-risk supplier as High/Critical would trigger unnecessary audits and strained relationships, but nobody would lose a production line over it.

**Track Two: Total Cost Prediction.** The CFO, Richard Huang, had a different but complementary need. Vanguard's annual procurement budget exceeded $800 million, and budget variance on individual purchase orders was a chronic headache. If procurement could predict total order cost with reasonable accuracy at the time of order placement, it would improve budget forecasting, support better negotiations with suppliers, and flag orders whose actual costs deviated sharply from predictions — a potential indicator of process breakdowns or pricing anomalies.

The cost data was inherently right-skewed: a center near $1,808 but a long tail stretching toward $500,000. Understanding what drove orders into that upper tail — whether it was order size, supplier region, product category, shipping method, or some interaction of these factors — would be as valuable as the point predictions themselves.

"Two models," Marco told his team. "One tells us which suppliers are going to hurt us. The other tells us which orders are going to cost more than we expected. Together, they give the board something actionable."

---

## V. The Geography Problem

It was during the third week of model development that Lena brought Marco a finding that complicated everything.

"I've been profiling supplier risk across every dimension in the dataset," she said, sliding a chart across his desk. "Product category, shipping method, order size, lead time — they all matter. But look at this." She pointed to the breakdown by supplier region.

The pattern was difficult to ignore. Suppliers from certain regions were systematically associated with higher risk classifications. The relationship held even after accounting for order characteristics, product categories, and shipping methods. From a purely predictive standpoint, `supplier_region` was among the most informative features in the classification model.

Marco studied the chart. "If we include region in the model, it improves accuracy."

"Substantially," Lena confirmed. "Region captures real supply chain dynamics — regulatory environments, infrastructure maturity, geopolitical stability, logistics complexity. There are legitimate reasons why risk profiles vary geographically."

"And illegitimate ones?"

Lena set the chart down. "Vanguard's historical procurement data reflects decades of sourcing decisions made by people with their own biases — conscious or not. If we trained the model on data where certain regions were under-invested, under-audited, or held to different standards, then the model isn't detecting genuine risk. It's encoding historical bias and calling it intelligence."

The implications were significant. Vanguard had made public commitments to supplier diversity, including expanding its sourcing from developing regions as part of its ESG strategy. A risk model that systematically flagged suppliers from those regions as high-risk could undermine diversity goals, concentrate procurement among a narrower set of established suppliers, and — perhaps most dangerously — create a self-fulfilling prophecy: suppliers flagged as risky would receive fewer orders, less investment in relationship-building, and fewer opportunities to demonstrate improved performance.

"But if we exclude region entirely," Lena continued, "the model loses a real signal. Some of the geographic variation *is* genuine — different regulatory frameworks, different infrastructure, different logistics networks. Throwing that away doesn't make the model fairer. It makes it less accurate, and less accurate models miss high-risk suppliers."

Marco leaned back. "So we can be accurate and potentially biased, or we can be fair and potentially blind."

"Or," Lena said, "we can try to find a middle path. But any middle path involves trade-offs that the board needs to understand and approve. This isn't a modeling decision. It's a policy decision."

---

## VI. Preparing for the Board

By the end of the second month, Marco and Lena had enough preliminary work to structure the board presentation. Marco outlined the agenda with the CFO and the Chief Procurement Officer, Sandra Yee.

The presentation would need to cover three areas.

First, **data quality and trustworthiness.** Before any model results, the Operations Committee needed to understand the limitations of the ERP data. The 30,000 missing records, the 50,000 entry errors, the 2,000 outliers — these were not footnotes. They were foundational constraints on what any model built from this data could reliably predict. Marco wanted the committee to understand that a risk model built on flawed procurement data would produce flawed risk scores, regardless of the sophistication of the algorithm.

Second, **predictive models and their limitations.** The supplier risk classifier and the cost regression model would be presented side by side, with transparent assessments of performance. Marco planned to show the committee where the models worked well, where they struggled, and — critically — the class imbalance problem in the risk data. With 55–60% of records in the High/Critical tier, the committee needed to understand what that distribution meant for model interpretation and operational deployment.

Third, **the geography question.** This was the discussion Marco dreaded most. The Operations Committee included two board members with strong views on ESG commitments and two with equally strong views on operational risk management. Presenting a model that used supplier region as a predictor without addressing the bias implications would be irresponsible. Presenting a model that excluded it without acknowledging the accuracy trade-off would be dishonest.

"The $14 million failure is the burning platform," Sandra Yee said during the prep meeting. "But the board will also ask: does this model create new risks while trying to prevent old ones?"

Marco didn't have a clean answer. He suspected the board wouldn't either — and that was precisely the conversation that needed to happen.

---

## Your Assignment

You have been retained as an external analytics consultant supporting Marco Reyes's initiative. Using Vanguard Manufacturing's one-million-record procurement dataset, you will work through four phases — mirroring the real-world arc of a supply chain analytics engagement: from data audit to board presentation.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Vanguard's ERP system was implemented in stages across regions, and the data carries the scars. Regional differences in data capture, inconsistent validation rules during rollout, and the daily pressures of a global procurement operation have left marks in the dataset. Your first task is to determine how deep those marks go.

**Guiding questions:**
- Where are the data quality issues concentrated — in specific supplier regions, product categories, or time periods? Do the missingness patterns align with the staggered ERP rollout narrative?
- How would you distinguish the ~2,000 genuine outliers from the ~50,000 entry errors? Under what circumstances would you impute missing values versus exclude records, and what are the downstream consequences of each choice?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, implausible metrics, entry errors, and distributional anomalies. For each issue, state what you found, quantify its scope, and recommend a handling strategy. This report should answer Marco's foundational question: *Is this data trustworthy enough to build a supplier risk model on?*

---

### Phase 2: The Prediction Challenge

Vanguard's board wants an early-warning system, and the CFO wants cost visibility. Two models. Ninety days.

#### Part A — Supplier Risk Classification

The board's mandate is a vendor pre-qualification system. Predict `supplier_risk` (4-class: Minimal / Low / Moderate / High-Critical).

**Guiding questions:**
- With roughly 55–60% of records in the High/Critical class and the smallest share in Minimal, this is a significantly imbalanced classification problem. What metric should you optimize — and why? What is the real-world cost of classifying a High/Critical supplier as Minimal versus flagging a Minimal-risk supplier as High/Critical?
- Identify the top features driving supplier risk classification. Which are leading indicators (observable before a failure) and which are lagging indicators (only available after problems have already occurred)?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with operationally appropriate metrics, and interpretation. Address the class imbalance and asymmetric misclassification costs explicitly. Conclude with a clear recommendation: which supplier attributes should procurement monitor as early-warning signals, and how would you embed this model into the vendor qualification workflow?

#### Part B — Total Cost Regression

The CFO needs accurate cost estimates at the time of order placement. Predict `total_cost`.

**Guiding questions:**
- Total cost is log-normally distributed with a center near $1,808 and a long right tail reaching $500,000. What drives orders into the upper tail? Which combinations of product category, supplier region, shipping method, and order characteristics produce the most expensive orders?
- How should procurement use cost predictions for budget forecasting, supplier negotiations, and anomaly detection? Where should the CFO trust the model, and where should he be skeptical?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (investigate the log-normal distribution and right tail), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to CFO Richard Huang: how should cost predictions inform procurement budgeting? Characterize the error distribution — where does the model perform well, and where does it struggle?

---

### Phase 3: The Ethical Crossroads

Lena's analysis revealed that supplier region is a powerful predictor of supplier risk. Including it improves classification accuracy. Excluding it may cause the model to miss genuinely high-risk suppliers. But using it may also encode historical procurement biases and undermine diversity commitments.

**Guiding questions:**
- Should the supplier risk model include `supplier_region` as a predictor? Construct arguments for both positions. What alternative approaches might capture legitimate geographic supply chain dynamics without encoding historical sourcing bias?
- If Vanguard deploys a risk scoring system that systematically flags suppliers from developing regions, what are the consequences for its ESG commitments, supplier diversity goals, and long-term supply chain resilience? Could the model create a self-fulfilling prophecy?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on the supplier-region question. Defend your position with both analytical evidence from the data and ethical reasoning. Address the counterargument directly. If you propose an alternative approach (e.g., decomposing region into its underlying risk factors, building region-specific models, or applying post-hoc fairness adjustments), specify exactly how it would work and what trade-offs it introduces.

---

### Phase 4: The Board Room

It is ninety days after the $14 million failure. Marco Reyes stands before Vanguard Manufacturing's Operations Committee and the Chief Procurement Officer. The board wants an early-warning system. The CFO wants cost visibility. The ESG committee wants assurance that the model won't undermine diversity commitments.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the Chief Procurement Officer, the CFO, two board members from the Operations Committee, and the head of ESG. Communicate: (a) the scope of Vanguard's supplier risk exposure, (b) what your models reveal about which suppliers are highest risk and what drives cost, (c) your recommended early-warning system design with implementation roadmap, and (d) the data limitations and model uncertainties the board should understand. Sandra Yee will ask: *"Does this model create new risks while trying to prevent old ones?"* Be ready.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in Vanguard's procurement data that is not covered by Phases 1–3? A regional pattern that warrants investigation, an unexpected interaction between supplier performance metrics, a temporal trend the ERP rollout doesn't fully explain, or a product category that defies the model's assumptions. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

| Resource | Path |
|---|---|
| Dataset | `datasets/supply_chain/synthetic_supplychain_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/supply_chain_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/supplychain_tasks.md` |

> The companion task set (`documentation/suggested_tasks/supplychain_tasks.md`) provides additional analytical questions — including unsupervised learning challenges such as supplier segmentation and order pattern clustering — that complement this case study. Students are encouraged to explore those tasks alongside the four phases above.

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Weakest Link." *From Data to Decisions*, Case 5. University of North Texas.
