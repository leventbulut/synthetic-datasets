# The Quiet Exodus

**A Data Science Case Study in Customer Strategy**

---

**From Data to Decisions** | Predicting the Quiet Exodus — E-Commerce Analytics

---

## I. The Number That Didn't Add Up

On a Monday morning in early October, Maya Chen arrived at Meridian Digital's downtown Austin headquarters to find a single sheet of paper centered on her desk. Someone from finance — she suspected the CFO's analyst — had printed a chart comparing quarterly revenue against site traffic for the past eighteen months. A handwritten note in red ink read: *"How do we explain this to the board?"*

The chart told a story that defied the playbook. Unique visitors were up 22% year-over-year. The marketing team had just wrapped its most successful influencer campaign to date. The brand's Instagram following had crossed two million. And yet revenue had barely moved — flat to within a rounding error of the prior quarter. The line for traffic climbed like a staircase; the line for revenue lay flat as a Kansas highway.

Maya had been VP of Customer Strategy at Meridian Digital for three years. The mid-size e-commerce company, which sold curated home goods and lifestyle products, had grown from a scrappy direct-to-consumer startup into a $240 million operation serving customers across North America. She'd seen soft quarters before. But this felt different. Customers weren't complaining. They weren't writing angry reviews or flooding the support queue. They were simply... leaving. Quietly. One abandoned cart at a time, one lapsed subscription after another, until the aggregate told a story that no individual data point revealed.

She called it "the quiet exodus."

## II. The Data Migration

The timing was either terrible or providential. Two weeks earlier, Meridian's data engineering team had completed a fourteen-month project to consolidate customer records from three legacy systems — the original Shopify instance from the company's founding, a Salesforce CRM bolted on during the Series B expansion, and a homegrown loyalty platform that a since-departed engineer had built in Django. The result was a single unified dataset: 600,000 customer records spanning 29 columns of behavioral, demographic, and transactional data.

Priya Sharma, Meridian's lead data engineer, had delivered the consolidated file with a caveat that Maya found both honest and unsettling. "The merge is done," Priya had written in a Slack message on September 23. "But I want to be transparent — some of these records came from systems with different validation rules. Some fields might be garbage. I'd recommend a thorough audit before anyone builds anything on top of this."

Maya pulled up the dataset on her second monitor. Six hundred thousand rows. Twenty-nine columns capturing everything from customer age and income to email engagement metrics, purchase frequency, average order values, satisfaction scores, and a five-tier loyalty segmentation — Diamond, Platinum, Gold, Silver, and Bronze. Two columns in particular caught her eye: a `churn_risk` classification (coded 0 for Low, 1 for Medium, 2 for High) and a continuous `customer_lifetime_value` variable. Both had been calculated by the legacy systems using rules that no one at Meridian fully understood anymore.

The churn numbers were sobering. Of the 600,000 customers in the dataset, 250,251 — fully 41.7% — were flagged as high churn risk. Another 142,134, or 23.7%, sat in the medium-risk category. Only 207,615 customers, about 34.6%, were classified as low risk. If those labels were even approximately correct, Meridian wasn't just experiencing a quiet exodus. It was hemorrhaging.

## III. Two Questions, One Dataset

The executive team convened on October 9 for a planning session that was supposed to focus on Black Friday promotions. It became something else entirely.

Derek Holt, Meridian's CEO, had seen the traffic-versus-revenue chart by then. He wanted answers before the holiday rush. "If 42% of our customers are at high risk of churning," he said, leaning forward in his chair, "I need to know which ones we can still save. I need an early-warning system. Before Black Friday. Before we spend another dollar acquiring people who are going to walk out the back door."

The ask was clear: build a classification model that could predict churn risk — Low, Medium, or High — using the behavioral and demographic signals in the CRM data. If the model could identify at-risk customers early enough, the retention team could intervene with targeted offers, personalized outreach, or loyalty incentives.

Simone Weiss, the CFO, had a different but complementary question. "We're going into budget season," she said. "Marketing is asking for $18 million in acquisition spend next year. I can't approve that without knowing what a customer is actually worth to us. Not what we hope they're worth. What the data says they're worth."

The customer lifetime value numbers in the dataset told their own story. Across 600,000 records, the mean CLV was $904, but the median — the number that better represented the typical customer — was only $816. The standard deviation of $401 meant enormous variability: some customers were worth multiples of the average, while others barely covered their acquisition cost. Simone wanted a regression model that could estimate CLV from observable customer attributes, giving the finance team a defensible basis for acquisition budgets and channel allocation.

Maya left the meeting with a mandate and a deadline: two models, one dataset, three weeks.

## IV. What the Data Revealed — and What It Concealed

Maya assembled a small cross-functional team: Priya from data engineering, a junior data scientist named Tomás Reyes, and an analyst from the marketing operations group. Their first task was to understand the dataset they'd been handed.

The 29 columns covered a broad landscape. Demographic attributes included age (mean of 38.2 years across the customer base) and income (mean of $36,010, though the median of $29,722 suggested a rightward skew from high earners pulling the average up). Behavioral metrics tracked email open rates, click-through rates, social media engagement, and mobile usage patterns. Transactional data captured purchase frequency, average order values, and returns. A satisfaction score on a 1-to-10 scale averaged 5.50 — precisely middling, which Maya found almost more alarming than a low number. "A 5.5 means nobody loves us and nobody hates us enough to say something," she observed. "That's exactly the kind of customer who just... drifts away."

The loyalty segmentation broke down unevenly: 152,200 Silver members, 142,587 Gold, 127,479 Bronze, 103,239 Platinum, and 74,495 Diamond. Maya noted that the smallest tier — Diamond, the highest-value loyalists — represented only about 12.4% of the base. If churn was disproportionately hitting that segment, the revenue implications would be severe.

But the dataset also carried the scars of its three-system heritage. Priya's warning about data quality proved prescient. Across the 600,000 records and 29 columns — over 17 million individual cells — the team identified 17,998 missing values. That amounted to roughly 0.10% of all data points, a number that sounded trivial in percentage terms but represented nearly 18,000 holes in the fabric of their customer understanding. Some columns appeared pristine. Others did not. The team would need to investigate which fields were affected, assess whether the missingness was random or systematic, and decide how to handle gaps before any model could be trusted.

"The question isn't just whether data is missing," Tomás said during their first working session. "It's whether it's missing in a way that will bias our predictions. If certain types of customers are more likely to have incomplete records, then any model we build on this data is going to inherit that bias."

## V. The Ethical Fault Line

By the second week of October, the team had made progress on both modeling tasks. But a discovery during feature exploration brought the project to a temporary halt.

Early analysis suggested that certain demographic attributes were among the stronger predictors of churn risk. The correlation wasn't perfect — no single variable told the whole story — but the signal was unmistakable. When Maya shared preliminary findings with the retention team, their response was immediate and enthusiastic. "Give us the list," said Jordan Blake, director of customer retention. "If we know who's most likely to leave, we can hit them with retention offers — discounts, free shipping, early access to the holiday collection."

Maya hesitated. "Think about what you're asking," she said. "If the model flags customers partly based on demographic characteristics, and we use that to target retention campaigns, we're essentially treating people differently based on who they are, not just what they've done. Is that personalization, or is it profiling?"

The room went quiet.

The question was genuinely ambiguous. On one hand, any predictive model — by definition — uses observable characteristics to forecast future behavior. That was the entire point. Retailers had been segmenting customers since the invention of the loyalty card. On the other hand, there was a meaningful difference between targeting a customer because their purchase frequency had declined and targeting them because they belonged to a demographic group that the model associated with higher churn. The first felt like responsive customer service. The second felt like something else.

Derek Holt, when briefed on the dilemma, framed it in business terms. "We lose $904 in expected lifetime value every time a customer walks away — more for our top segments. If we have the data to prevent that, I'm not sure we can afford *not* to act on it." Simone Weiss raised the counterpoint: "And if it gets out that we're differentially targeting customers based on demographics? The PR risk alone could cost us more than the churn."

Maya found herself caught between competing obligations — to the company's financial health, to its customers' trust, and to a dataset that didn't come with an instruction manual for ethical interpretation. The models could predict. Whether the predictions should be acted upon — and how — was a human question.

## VI. The Board Presentation

On October 28, four days before Halloween and twenty-nine days before Black Friday, Maya stood before Meridian Digital's board of directors. Her presentation carried a simple title: *The Quiet Exodus — Who We're Losing, Why, and What It Will Cost.*

She had the models. She had the numbers. She had a dataset of 600,000 customers whose behaviors, preferences, and risks had been quantified across 29 dimensions. What she didn't have was certainty — about the data's completeness, about the models' fairness, or about the right way to balance prediction with principle.

The board would have questions. Maya was ready to answer some of them. Others, she knew, would require the kind of judgment that no algorithm could provide.

---

## Your Assignment

You have been brought in as a data science consultant supporting Maya Chen's team. Using Meridian Digital's 600,000-record CRM dataset, you will work through four phases — mirroring the real-world arc of a data science engagement: from raw data to boardroom recommendation.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Maya's team knows the dataset carries scars from its three-system migration. Your first task is to determine how deep those scars go — and whether the data is trustworthy enough to build on.

**Guiding questions:**
- The dataset contains 17,998 missing values across 29 columns. Where is the missingness concentrated — in specific columns, customer segments, or loyalty tiers? Is the pattern random or systematic?
- Beyond missing values, what other data quality issues might arise from merging three legacy systems with "different validation rules"? Design an EDA plan that would surface problems before model training begins.
- The mean income is $36,010 while the median is $29,722. What does this discrepancy reveal about the distribution, and how might it affect model performance?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). For each issue you discover, state what you found, assess its likely cause, quantify its scope, and recommend a handling strategy (impute, cap, flag, remove, or leave as-is). Justify your choices. This report should give Maya's team confidence — or warranted caution — about the data foundation beneath their models.

---

### Phase 2: The Prediction Challenge

Maya has two mandates, one dataset, and three weeks.

#### Part A — Churn Risk Classification

The CEO wants an early-warning system before Black Friday. Predict `churn_risk` (Low / Medium / High).

**Guiding questions:**
- The churn risk variable has three levels: Low (34.6%), Medium (23.7%), and High (41.7%). How would you handle this moderate class imbalance? What evaluation metrics are most appropriate when the cost of missing a high-risk customer exceeds the cost of a false alarm?
- The average satisfaction score is 5.50 on a 1-to-10 scale — "precisely middling." What challenges does a feature with low variance near the midpoint present? How might you engineer more predictive features from satisfaction data?
- Design a feature engineering strategy. Which raw columns might benefit from transformation, interaction terms, or binning? How would you validate that engineered features improve performance without introducing data leakage?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, training of at least two distinct algorithms, evaluation with business-appropriate metrics, and interpretation. Address the class imbalance explicitly. Conclude with a plain-language summary: which customers are most at risk, and what signals should Maya's retention team watch for?

#### Part B — Customer Lifetime Value Regression

The CFO needs CLV estimates to set the $18 million acquisition budget. Predict `customer_lifetime_value`.

**Guiding questions:**
- The CLV distribution has a mean of $904, a median of $816, and a standard deviation of $401. Sketch the likely shape. What regression approaches would you consider, and should the target variable be transformed?
- How would you translate regression predictions into actionable budget recommendations? What level of accuracy is "good enough" for financial planning, and how would you communicate uncertainty to non-technical stakeholders?
- The loyalty tiers are unevenly distributed (Diamond: 74,495 to Silver: 152,200). Should tier membership be a feature, or should separate models be trained per tier?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (mean $904, median $816 — what does this shape tell you?), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to CFO Simone Weiss: how should CLV predictions inform the $18 million acquisition budget? Where is the model most and least reliable?

---

### Phase 3: The Ethical Crossroads

Maya's team discovered that demographic attributes are among the stronger predictors of churn risk. The retention team wants the list. Maya hesitates.

**Guiding questions:**
- If demographic characteristics predict churn, how would you assess whether the model's predictions are fair across demographic groups? What specific fairness metrics would you compute, and what thresholds would you apply?
- Derek Holt argues the company "can't afford not to act." Simone Weiss warns about PR risk. Construct arguments for both positions. Is there a middle path that uses predictions while mitigating the ethical concerns?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position: Should Meridian use demographic-based churn predictions to target retention campaigns? Defend your position with both analytical evidence from the data and ethical reasoning. If you propose a middle path, specify exactly how it would work in practice — vague compromises will not be accepted.

---

### Phase 4: The Board Room

It is October 28 — twenty-nine days before Black Friday. Maya stands before the board.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the CEO, CFO, head of marketing, and two independent board members with no data science background. Communicate: (a) the scale of the churn problem and its financial impact, (b) what your models reveal about who is leaving and why, (c) your recommended course of action, and (d) what the data *cannot* tell them. No jargon. No confusion matrices. Translate technical findings into business decisions.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in the data that is not covered by Phases 1–3? An unexpected pattern, a hidden segment, a counterintuitive relationship, a limitation that changes everything, or an opportunity that Maya's team hasn't considered. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

## Data Resources

| Resource | Path |
|---|---|
| Customer Dataset | `datasets/marketing/synthetic_marketing_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/marketing_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/marketing_tasks.md` |

Students should begin by loading the dataset and performing independent exploratory data analysis before engaging with the discussion questions. The data dictionary provides complete column definitions, data types, and valid value ranges.

---

## Exhibits

- **[Exhibit A](exhibits/exhibit_A.md)** — Internal email from CMO Diane Kowalski to the executive team regarding customer attrition patterns
- **[Exhibit B](exhibits/exhibit_B.md)** — Meridian Digital Q3 KPI Dashboard snapshot

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2025 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2025). "The Quiet Exodus." *From Data to Decisions*, Case 1. University of North Texas.
