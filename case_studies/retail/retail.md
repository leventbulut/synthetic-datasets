# The Wrong List

**A Data Science Case Study in Customer Segmentation**

---

**From Data to Decisions** | Unmasking the Wrong VIP List — Retail Analytics

---

## I. Forty Percent

The slide should not have existed. It was a single scatter plot — hand-selected VIP customers on the x-axis, data-ranked CLV customers on the y-axis — and it had been buried in an appendix that no one was supposed to read until the quarterly business review. But Evergreen Retail Group's CEO, Catherine Yoo, had a habit of reading appendices. She had pulled David Park aside in the hallway outside the third-floor conference room on a Tuesday morning in late January, held up her tablet, and asked a question that would consume the next three months of his professional life.

"David, why do only 40% of the names on these two lists match?"

David Park had been VP of Customer Analytics at Evergreen Retail Group for four years. The company operated 340 stores across four formats — Discount, Standard, Premium, and Luxury — serving a loyalty program base of 800,000 members. Evergreen had grown through acquisition: the Discount chain came first, a scrappy regional player with 180 locations; Standard was absorbed eighteen months later; Premium followed within the year. The Luxury division, a boutique operation with just 22 stores, was the most recent addition. Each acquisition brought its own point-of-sale system, its own CRM, and its own definition of what made a customer valuable.

The VIP list — 47,000 names, curated quarterly by regional store managers — was Evergreen's crown jewel of personalization. VIP customers received early access to seasonal collections, invitations to in-store events, handwritten thank-you notes from department leads, and a dedicated concierge line. The program cost $4.2 million annually to operate. And according to the scatter plot that Catherine Yoo was now holding six inches from David's face, more than half of those dollars were being spent on people who were not, by any quantitative measure, the company's most valuable customers.

"The managers pick VIPs based on relationships," David said carefully. "Regulars they recognize. People who are pleasant to deal with. Customers who buy visibly — big shopping bags, high-ticket items."

"And the data says?"

"The data says value is more nuanced than visibility."

## II. Eight Hundred Thousand Scars

David's team pulled the consolidated dataset the following week. Eight hundred thousand transaction records. Twenty-two columns spanning demographics, purchase behavior, loyalty program activity, and channel preferences. The file was large, and it was ugly.

Evergreen's CRM had been stitched together from three separate acquisitions over two years — three POS systems with different field definitions, different validation rules, and different tolerance for human error. The Discount chain's legacy system had been built in-house by a contractor who left no documentation. The Standard chain ran a mid-tier SaaS platform that enforced some data validation but not enough. The Premium and Luxury divisions shared an enterprise CRM that was technically sophisticated but had been configured by people who no longer worked at the company.

The scars were everywhere.

Anika Vasquez, the senior data engineer who had overseen the consolidation, briefed David's team on a Wednesday afternoon. "I can tell you where the bodies are buried," she said, pulling up a summary on the conference room monitor. "About 24,000 records — roughly 3% of the file — have missing values in fields like annual income, satisfaction scores, return rates, loyalty points, and online purchase percentage. And I can tell you right now: the missingness isn't random. It follows patterns."

She paused. "But that's not what keeps me up at night."

The entry errors were worse. Approximately 40,000 records — 5% of the dataset — contained values that were physically impossible or logically implausible. Basket sizes of 50, 80, even 150 items per transaction. Days-since-last-visit values that were negative — customers apparently visiting stores before their last visit, temporal paradoxes courtesy of a timezone mismatch in the Discount chain's legacy system. Visit frequencies suggesting some customers were shopping 60 to 200 times per month, which would require visiting a store multiple times per day, every day, including holidays.

"The Discount system stored visit dates in local time without timezone metadata," Anika explained. "When we merged it with the Standard system, which used UTC, some date arithmetic went sideways. The negative days-since-last-visit values are almost certainly a conversion artifact. The inflated visit frequencies? I suspect some of those are loyalty card scans at gas pumps and pharmacy counters getting counted as store visits."

Beyond the missing values and entry errors, a smaller but more treacherous population lurked in the tails. Roughly 1,600 records — just 0.2% of the dataset — contained extreme outliers: transaction amounts between $20,000 and $80,000, average item prices reaching $5,000, annual incomes exceeding $800,000 and climbing as high as $3 million. Some of these might be legitimate — a Luxury-format customer purchasing a high-end watch, a high-net-worth individual whose income was genuinely extraordinary. Others might be keystroke errors, decimal-point slips, or artifacts of bulk corporate purchases incorrectly attributed to individual customer records.

"The data is real in the sense that it came from real systems," Anika told the team. "Whether it's *accurate* is a different question entirely."

## III. Two Targets, One Truth

David presented the data landscape to the executive team during the first week of February. The meeting had been scheduled for thirty minutes. It ran ninety.

Marcus Webb, the Chief Merchandising Officer who oversaw the VIP program, was the first to push back. "I've been in retail for twenty-two years," he said. "My store managers know their customers. They see them every week. They know their kids' names. You're telling me an algorithm is going to do that better?"

"I'm telling you the algorithm and your managers agree on 40% of VIP customers," David replied. "The question is what's happening with the other 60%."

Catherine Yoo cut through the debate. "I want two things. First: build me a segmentation system that classifies every customer — all 800,000 — into Budget, Moderate, Premium, or VIP based on what the data actually shows, not what a store manager remembers from last Thursday. Second: predict lifetime value. If we're spending $4.2 million on a personalization program, I want to know the expected return on every dollar."

The classification target was `customer_segment` — a four-class variable coded 0 through 3: Budget, Moderate, Premium, and VIP. The current distribution, inherited from the legacy systems' own segmentation logic, showed a pyramid structure that Marcus Webb considered healthy and David Park considered suspicious. The precise breakdown was something the team would need to verify from the data — and reconcile with the 47,000-name VIP list that the store managers maintained independently.

The regression target was `customer_lifetime_value` — a continuous variable representing the estimated long-term revenue contribution of each customer. The values spanned a wide range, from a floor around $20 to a ceiling near $15,000, with a distribution that David suspected was heavily right-skewed. A small number of customers were worth orders of magnitude more than the median. Understanding *which* customers, and *why*, would determine how Evergreen allocated its personalization budget.

"We have 22 variables to work with," David told the team. "Demographics — age, gender, income. Store and product data — which format they shop, what categories they buy. Behavioral signals — basket size, item prices, transaction amounts, visit frequency, recency. Loyalty engagement — membership status, points balances, online purchase rates, return rates, discount sensitivity, satisfaction scores. Payment methods, referral sources, transaction dates."

He looked around the table. "The dataset is large enough to be useful and messy enough to be dangerous. We need to clean before we build."

## IV. The Variable That Changed Everything

By the third week of February, David's team had made meaningful progress on both modeling tasks. They had developed cleaning protocols for the entry errors, imputation strategies for the missing values, and initial feature engineering pipelines. Two junior analysts were running classification experiments; a third was building regression benchmarks. The work was methodical, unglamorous, and exactly on schedule.

Then Priya Osei, the team's most experienced data scientist, walked into David's office and closed the door.

"I need to show you something about the feature importance rankings," she said.

The classification model — the one designed to replace the gut-feel VIP list with data-driven segmentation — was performing well. But the features driving its predictions told an uncomfortable story. Annual income and store type were among the strongest predictors of customer segment. Customers who shopped at Luxury and Premium formats, and who reported higher incomes, were far more likely to be classified as Premium or VIP. Customers at Discount formats with lower incomes were overwhelmingly classified as Budget.

"That's not surprising," David said. "Income correlates with spending power. Spending power correlates with lifetime value. That's the whole point of segmentation."

"Right," Priya said. "But follow the logic one step further. If we deploy this model and use it to drive the personalization program — the concierge line, the event invitations, the handwritten notes — we're essentially building a system that gives better service to wealthier customers and worse service to poorer ones. And we're doing it automatically, at scale, with an algorithm that nobody on the store floor will understand or be able to question."

David stared at the feature importance chart on Priya's laptop.

"I talked to Sandra Kim in D&I," Priya continued. Sandra Kim was Evergreen's Director of Diversity and Inclusion. "She raised a question I can't stop thinking about. She asked: 'Is personalization just a polite word for discrimination?'"

The question hung in the air.

The argument for using income and store type was straightforward and defensible. These variables reflected real differences in customer behavior and value. Ignoring them would produce a less accurate model, which would lead to less efficient resource allocation, which would ultimately hurt the business and, by extension, the employees and communities it supported. Personalization, by its very nature, meant treating different customers differently. That was the entire value proposition.

The argument against was equally compelling. Evergreen served communities across the socioeconomic spectrum. Its Discount format was a lifeline for budget-conscious families. If the algorithm systematically deprioritized those customers — routing them to automated phone trees while Premium and Luxury shoppers got the concierge line — the company would be creating a two-tier experience stratified by wealth. And unlike the old system, where a store manager's judgment could be questioned, challenged, and overridden, an algorithmic classification would operate invisibly, at scale, with the veneer of objectivity.

"There's a middle path," David said slowly, though he wasn't sure he believed it yet. "We could build the model with those features for accuracy but implement guardrails on how the predictions are used."

Priya raised an eyebrow. "Guardrails designed by whom? Enforced by whom? Audited how often?"

## V. The Presentation

On a Friday afternoon in early March, David stood before Evergreen's Customer Experience Committee — Catherine Yoo, Marcus Webb, CFO Robert Tanaka, Sandra Kim from D&I, and two independent board members who had flown in from the East Coast.

His presentation was titled *The Wrong List: What 800,000 Transactions Tell Us About Who Our Best Customers Really Are.*

He had the models. He had segmentation predictions for every customer in the database. He had CLV estimates with confidence intervals. He had a feature importance analysis that explained *why* the models made the predictions they did. And he had an ethical framework that raised more questions than it answered — about fairness, about transparency, about what it meant to be a company that promised "personalized service for every customer" while operating an algorithm that allocated personalization based partly on income.

Marcus Webb would ask whether the data-driven segments should replace or supplement the store managers' judgment. Robert Tanaka would want to know the dollar impact — how much revenue was being left on the table by the current VIP list, and how much could be captured by a more accurate one. Sandra Kim would press on the equity implications. Catherine Yoo would want a recommendation, not a hedge.

David had twenty-two columns of data, 800,000 rows, and no easy answers.

---

## Your Assignment

You have been brought in as a data science consultant supporting David Park's team. Using Evergreen Retail Group's 800,000-record transaction dataset, you will work through four phases — mirroring the real-world arc of a data science engagement: from raw data to boardroom recommendation.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Evergreen's CRM was stitched together from three acquisitions — three POS systems, three sets of validation rules, and three different tolerance levels for data quality. Your first task is to determine how deep those scars go.

**Guiding questions:**
- The dataset contains approximately 24,000 records with missing values across five fields. Where is the missingness concentrated — in specific columns, store types, or customer segments? Is the pattern random or systematic, and what does it suggest about the legacy systems that generated this data?
- Beyond missing values, the team has flagged roughly 40,000 entry errors — negative days-since-last-visit, basket sizes exceeding 100, and visit frequencies suggesting customers shop multiple times per day. How would you identify, quantify, and handle these anomalies? What cleaning strategy preserves information while removing noise?
- Approximately 1,600 records contain extreme outliers in transaction amounts, item prices, and income. How would you distinguish legitimate high-value transactions from data errors? What are the consequences of each decision — keeping, capping, or removing — for model performance?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). For each issue you discover, state what you found, assess its likely cause, quantify its scope, and recommend a handling strategy (impute, cap, flag, remove, or leave as-is). Justify your choices. This report should give David's team confidence — or warranted caution — about the data foundation beneath their models.

---

### Phase 2: The Prediction Challenge

David has two mandates, one dataset, and a CEO who reads appendices.

#### Part A — Customer Segment Classification

Replace the gut-feel VIP list with a data-driven segmentation system. Predict `customer_segment` (Budget / Moderate / Premium / VIP — coded 0 through 3).

**Guiding questions:**
- The customer segment variable has four classes with a distribution that reflects Evergreen's pyramid structure. How would you evaluate a 4-class classifier where the business cost of misclassifying a VIP as Budget far exceeds the cost of the reverse error? What metrics capture this asymmetry?
- Store type and annual income are strong predictors of segment membership — but using them raises ethical concerns explored in Phase 3. From a purely technical standpoint, how does including or excluding these features affect model performance? What does this tell you about the information content of the remaining variables?
- Design a feature engineering strategy that leverages the behavioral and transactional variables. Which combinations — spending per visit, recency-frequency-monetary composites, loyalty engagement ratios — might create signals that are both predictive and less ethically fraught than raw income?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, training of at least two distinct algorithms, evaluation with business-appropriate metrics, and interpretation. Address the multi-class challenge explicitly. Conclude with a plain-language summary: how does the data-driven segmentation compare to the store managers' VIP list, and what does the 40% overlap (or lack thereof) reveal?

#### Part B — Customer Lifetime Value Regression

Predict how much each customer is worth over the long term. Predict `customer_lifetime_value`.

**Guiding questions:**
- The CLV distribution spans from approximately $20 to $15,000. Given the likely right-skewed, log-normal shape, what regression approaches would you consider? Should the target variable be transformed before modeling, and how does this affect interpretability?
- The dataset captures both behavioral signals (basket size, visit frequency, transaction amounts) and attitudinal indicators (satisfaction scores, discount sensitivity, loyalty engagement). How would you assess which category of features drives more predictive power for CLV? What are the implications for Evergreen's strategy?
- How would you translate regression predictions into actionable personalization budgets? If the VIP concierge program costs $4.2 million annually for 47,000 customers (~$89 per customer), what CLV threshold justifies the investment?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis, preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to CFO Robert Tanaka: what is the expected return on the $4.2 million VIP program, and how should it be restructured based on CLV predictions?

---

### Phase 3: The Ethical Crossroads

Priya Osei's feature importance analysis revealed that annual income and store type are among the strongest predictors of both customer segment and lifetime value. Sandra Kim from D&I asks: *Is personalization just a polite word for discrimination?*

**Guiding questions:**
- If income-based features are included in the segmentation model, how would you assess whether the resulting customer experience is equitable across socioeconomic groups? What specific fairness metrics would you compute, and what disparities would trigger concern?
- Evergreen's Discount format serves budget-conscious communities that may already face systemic disadvantages. If the algorithm systematically classifies Discount shoppers as "Budget" and routes them to lower-tier service experiences, is the company reinforcing existing inequities — even if the predictions are statistically accurate? Construct arguments for both positions.

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position: Should Evergreen use income and store-type features in its customer segmentation model? Defend your position with both analytical evidence from the data and ethical reasoning. If you propose a middle path — such as using these features for prediction but implementing guardrails on how predictions are operationalized — specify exactly what those guardrails would be, who would enforce them, and how they would be audited. Vague compromises will not be accepted.

---

### Phase 4: The Board Room

It is early March. David stands before the Customer Experience Committee.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the CEO, CFO, Chief Merchandising Officer, the D&I Director, and two independent board members with no data science background. Communicate: (a) the scale of the VIP misalignment problem and its financial impact, (b) what your models reveal about who the most valuable customers actually are, (c) your recommended restructuring of the personalization program, and (d) what the data *cannot* tell them. No jargon. No confusion matrices. Translate technical findings into business decisions.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in the data that is not covered by Phases 1–3? An unexpected pattern in how product categories drive lifetime value, a hidden relationship between payment methods and loyalty, a segment that the four-class system misses entirely, or a channel preference shift that Evergreen hasn't noticed. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

## Data Resources

| Resource | Path |
|---|---|
| Transaction Dataset | `datasets/retail/synthetic_retail_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/retail_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/retail_tasks.md` |

Students should begin by loading the dataset and performing independent exploratory data analysis before engaging with the discussion questions. The data dictionary provides complete column definitions, data types, and valid value ranges. The companion task set offers additional analytical exercises that extend and complement the case narrative.

---

## Exhibits

- **[Exhibit A](exhibits/exhibit_A.md)** — Internal memo from CMO Marcus Webb regarding VIP program overlap analysis
- **[Exhibit B](exhibits/exhibit_B.md)** — Evergreen Retail Group Customer Analytics Dashboard

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2025 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2025). "The Wrong List." *From Data to Decisions*, Case 7. University of North Texas.
