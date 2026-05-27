# The Route That Broke the Contract

**A Data Science Case Study in Logistics Prediction and Workforce Equity**

---

**From Data to Decisions** | When Your Largest Client Walks and the Clock Starts Ticking — Transportation Analytics

---

## I. The Phone Call That Changed Everything

On a Thursday morning in early January, Nina Volkov arrived at the third-floor operations center of Apex Logistics to find a voicemail from someone she had hoped would never call directly. The voice belonged to David Hargrove, Vice President of Logistics at Ridgeline Retail — Apex's largest client, representing roughly 18% of annual revenue — and the message was brief. "Nina, I'm sending a formal letter today. We're moving our business to another carrier effective end of quarter. I wanted you to hear it from me first."

Nina had been Director of Fleet Operations at Apex Logistics for six years. The company — a regional freight and last-mile delivery operation running a mixed fleet of bikes, vans, trucks, and heavy trucks across urban, suburban, and highway corridors — handled approximately 450,000 deliveries per year and had built its reputation on reliability. That reputation had eroded badly over the previous quarter. The holiday season had been a disaster. On-time delivery rates, which Apex had historically maintained above 90%, had dropped below 80%. Ridgeline's customers — the ones whose packages arrived late, or damaged, or not at all — didn't know Apex's name. They knew Ridgeline's. And Ridgeline's customer satisfaction scores had cratered accordingly.

Hargrove's letter arrived by courier that afternoon (*see* **Exhibit A**). It was worse than the voicemail had suggested. Ridgeline wasn't just leaving — they were quantifying the damage. The letter cited specific on-time performance numbers, broken down by delivery priority and weather condition. It identified the holiday corridor between late November and late December as the point of failure. And it closed with a conditional offer: if Apex could demonstrate — within sixty days — a working predictive system capable of flagging at-risk shipments before they left the warehouse, Ridgeline would consider reinstating the contract on a probationary basis.

Nina brought the letter to Apex's CEO, Thomas Brennan, that evening. Brennan read it twice, set it on his desk, and said: "You have sixty days. Build the system or start looking for a buyer."

## II. Four Hundred Fifty Thousand Deliveries

By the following Monday, Nina had pulled a full data extract from Apex's Transportation Management System. The result was a dataset of 450,000 delivery records spanning nearly three years of operations — every route dispatched, every package tracked, every outcome logged — captured across 22 columns.

The columns painted a comprehensive picture. Route characteristics included distance (centered around 90 kilometers, though the range extended from 5-kilometer urban bike deliveries to 2,000-kilometer long-haul freight runs), load weight (median roughly 665 kilograms, spanning from single-kilogram envelope deliveries to 10,000-kilogram heavy freight), and the number of stops per route (typically three or four, but occasionally as many as twenty-five for dense urban multi-drop routes). Vehicle data tracked the fleet's composition — Bikes, Vans, Trucks, and Heavy Trucks — along with fuel efficiency (centered around 8 km/L), maintenance scores on a 30-to-100 scale (mean approximately 70), and fuel costs. Driver metrics captured experience in years (centered around 4.5 years, ranging from half a year to three decades) and customer ratings on a 1-to-5 scale (mean roughly 3.5). Environmental factors logged route type (Urban, Suburban, Highway), weather conditions at dispatch (Clear roughly half the time, Rain about a quarter, Snow and Fog splitting the remainder), and traffic density as a ratio between 0.1 and 0.95. Delivery priorities were tagged as Standard, Express, or Same Day. Package condition upon arrival was recorded as Perfect, Good, Minor Damage, or Damaged.

Two columns anchored the analytical challenge ahead.

The first was `delivery_success`, a three-class outcome variable — On Time, Minor Delay, and Major Delay — that encoded the result of every delivery against its promised window. This was the variable Hargrove's letter had made existential. If Apex couldn't predict which shipments were likely to fail before they left the dock, no amount of after-the-fact apology would save the Ridgeline contract — or the ones that would follow it out the door.

The second was `delivery_cost`, a continuous variable representing the fully loaded cost of each delivery. The distribution was log-normal, centered around roughly $33 but extending from $5 for short urban bike runs to more than $8,000 for long-haul heavy freight in adverse conditions. Apex's pricing model was based on flat rate tables that hadn't been updated in two years. If the actual cost of a delivery could be estimated dynamically at dispatch, the company could price its services accurately — and stop hemorrhaging margin on routes it was unknowingly subsidizing.

Raj Patel, Nina's analytics lead, began the data audit on Tuesday and had his first concerns by Wednesday. "The TMS has its own ideas about data quality," he told Nina during a working session. "We've got delay_minutes entries showing negative values — sometimes minus ten minutes, sometimes minus a hundred. The system was recording early arrivals as errors because the validation rule only expected positive integers. The num_stops field has entries of fifty, sixty, even eighty for single routes — those are almost certainly phantom scans from the barcode system doubling or tripling stop counts. And some of the actual_duration_hours records suggest drivers were on the road for seventy hours. A hundred hours. One record shows two hundred hours — that's more than a week of continuous driving."

The scope of the data quality challenges crystallized over the next several days. Across the 450,000 records and 22 columns, approximately 13,500 records — about 3% — carried missing values concentrated in fuel efficiency, driver rating, maintenance score, traffic density, and fuel cost. The missingness wasn't random. It tracked patterns a careful analyst would need to identify. Beyond the missing values, roughly 22,500 records — 5% of the dataset — contained entry errors: delay_minutes showing negative values from −10 to −100, num_stops inflated to 30–80 per route, and actual_duration_hours stretching to 70, 100, even 200 hours. And then there were the outliers — approximately 900 records, just 0.2% of the total, with distances between 5,000 and 15,000 kilometers (further than the continent is wide), load weights between 20,000 and 80,000 kilograms (heavier than anything in Apex's fleet could carry), or fuel costs between $5,000 and $15,000 for a single delivery. Sensor glitches? Decimal point errors? Legacy data from a test environment that never got purged? The TMS couldn't say.

"The question," Raj said, "is whether we can build something trustworthy on top of this. Ridgeline isn't going to accept 'our data was messy' as an answer."

## III. The Feature That Split the Room

By the third week, Nina's team had moved from diagnosis to modeling. The classification challenge — predicting `delivery_success` across three levels — demanded a system that could flag at-risk shipments at dispatch, before a single wheel had turned. The regression challenge — estimating `delivery_cost` to support dynamic pricing — demanded a model that could replace the flat rate tables with route-specific estimates accurate enough to protect margin without losing bids.

Early results were encouraging. The classification models achieved meaningful separation across the three outcome categories, and the regression models captured the log-normal cost distribution with reasonable fidelity. But a discovery during feature importance analysis brought the project to a confrontation that Nina hadn't anticipated.

One variable — `driver_experience_years` — consistently appeared as the strongest predictor of on-time delivery. The signal was clean, persistent across every algorithm the team tested, and operationally intuitive: experienced drivers knew the routes, anticipated the delays, managed the exceptions. From a pure prediction standpoint, it was the single most valuable feature in the model.

The implication was immediate. If Apex deployed the model for route assignment — sending the highest-risk shipments to the most experienced drivers — it would almost certainly improve on-time rates. It was, in the most literal sense, optimization. Assign the best drivers to the hardest routes. Watch the metrics climb.

Marco DeSilva, the operations manager, was the first to advocate. "This is exactly what the system should do," he said during a cross-functional review. "We match skill to difficulty. Every airline does it. Every hospital does it. You don't put the intern on the complex surgery."

Carmen Reyes, the local Teamsters representative, was the one who objected. She had been invited to the review as a courtesy — Apex's collective bargaining agreement required consultation on any change to route assignment protocols — and she had listened quietly until DeSilva finished.

"What you're describing," she said, "is a caste system. Senior drivers get the easy routes — the ones with high on-time rates, the ones that earn performance bonuses, the ones that build the track record for promotion. Junior drivers get the difficult routes — the ones with weather delays and traffic congestion and tight windows. They get the blame when the package is late. They get the poor ratings. They get stuck. And the model you're building will make it look like the system is fair, because the data will confirm that junior drivers perform worse — on the routes you assigned them precisely because you expected them to perform worse."

The room went quiet.

Nina understood both arguments. DeSilva was right that matching driver capability to route difficulty would improve aggregate performance — the data supported it unambiguously. Reyes was right that doing so would create a self-reinforcing loop: experienced drivers would accumulate the metrics that justified continued preferential treatment, while junior drivers would accumulate the metrics that justified continued assignment to difficult routes. The model wouldn't create the inequality from scratch — experience genuinely predicted performance — but it would institutionalize it, accelerate it, and wrap it in the language of data-driven objectivity.

"You're asking me to choose between a system that optimizes for the number and a system that's fair to the people behind the number," Nina said.

Carmen didn't blink. "I'm asking you to understand that those might not be different choices. They might just be different timelines."

## IV. Sixty Days

The calendar compressed everything. In fifty-three days, Nina would present to Thomas Brennan and, if the CEO approved the system, to David Hargrove in a contract reinstatement meeting that Ridgeline had agreed to schedule — contingent on a credible demonstration.

Brennan wanted results. Could the model predict which shipments would fail before dispatch? Could dynamic pricing recover the margin Apex was losing on underpriced routes? Was the system ready for a client-facing demonstration? He would ask questions in operational language and expect answers with financial projections.

Hargrove wanted proof. What was the model's accuracy across delivery priorities? How would it perform in adverse weather — the exact conditions that had destroyed the holiday season? Had the data quality issues been addressed or merely papered over? Hargrove would ask questions in the language of a logistics executive who had been burned, and he would expect answers with specificity and humility.

Nina stood at the intersection of two conversations — one about winning back a contract, one about building a system her drivers could trust — knowing that a misstep in either room could end the company. A model that satisfied Brennan's demand for performance might fail Reyes's test of fairness. A model that satisfied Reyes's principle of equity might fail Hargrove's demand for prediction accuracy. And somewhere in the data — 450,000 deliveries, 22 columns, 13,500 missing values, 22,500 entry errors, and one feature that worked too well — lay the answers that both audiences needed but neither might want to hear.

She opened her laptop, pulled up the operations dashboard (*see* **Exhibit B**), and began to build the case.

---

## Your Assignment

You have been engaged as an external data science consultant by Apex Logistics' operations analytics group. Using the company's 450,000-record delivery dataset, you will work through four phases — mirroring the real-world arc of a high-stakes predictive analytics engagement: from raw data to boardroom and client presentation.

The companion task set (`documentation/suggested_tasks/transportation_tasks.md`) provides structured analytical exercises aligned with this case. The phases below frame those tasks within the narrative and ethical context that a working data scientist at Apex would face.

---

### Phase 1: Discovery & Diagnosis

Before any prediction system can be trusted, the data must be understood.

Nina's team knows the TMS dataset carries the artifacts of years of sensor glitches, barcode errors, and validation rule failures. Your first task is to determine how deep those problems go — and whether the data is reliable enough to build on.

**Guiding questions:**
- The dataset contains approximately 13,500 records with missing values (~3% of deliveries), concentrated in several operational fields. Is this missingness random, or does it follow a pattern tied to vehicle type, route characteristics, or other operational attributes? What are the implications for any downstream model?
- Beyond missing values, the team has flagged entry errors in delay minutes, number of stops, and actual duration hours, as well as outliers in distance, load weight, and fuel cost. Design an EDA plan that would surface the full scope of these issues before model training begins.
- Delivery cost follows a log-normal distribution centered around roughly $33, yet the range extends from $5 to well beyond $8,000. What does this shape reveal about the fleet's operating profile, and how might extreme values affect model performance?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). For each issue you discover, state what you found, assess its likely cause (sensor error, barcode duplication, validation rule failure, or genuine operational variation), quantify its scope, and recommend a handling strategy (impute, cap, flag, remove, or leave as-is). Justify your choices. This report must be defensible to both internal stakeholders and a prospective client evaluating Apex's analytical capabilities.

---

### Phase 2: The Prediction Challenge

Nina has two mandates, one dataset, and fifty-three days before the Ridgeline meeting.

#### Part A — Delivery Success Classification

Ridgeline will evaluate whether Apex can predict delivery outcomes before dispatch. Predict `delivery_success` (On Time / Minor Delay / Major Delay — three classes).

**Guiding questions:**
- The delivery success variable has three levels. Examine the class distribution in the data. How would you handle any imbalance, and what evaluation metrics are most appropriate when the operational cost of failing to flag a Major Delay exceeds the cost of a false alarm?
- Driver experience averages around 4.5 years, but the range spans 0.5 to 30 years. Weather conditions shift from Clear to Snow and Fog. Traffic density ranges from 0.1 to 0.95. How do these features interact to affect delivery outcomes, and which interactions would you engineer explicitly?
- Design a feature engineering strategy. Which raw columns might benefit from transformation, interaction terms, or binning? How would you validate that engineered features improve performance without introducing data leakage from post-dispatch variables?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, training of at least two distinct algorithms, evaluation with business-appropriate metrics, and interpretation. Address any class imbalance explicitly. Conclude with a plain-language summary: which shipments are most likely to fail, and what dispatch-time signals should Apex's operations team watch for?

#### Part B — Delivery Cost Regression

The pricing team needs dynamic cost estimates to replace the flat rate tables. Predict `delivery_cost` (continuous).

**Guiding questions:**
- Delivery cost spans from $5 to over $8,000 with a log-normal distribution centered around $33. What regression approaches would you consider, and should the target variable be transformed? How would you handle the extreme right tail of high-cost deliveries?
- How would you translate regression predictions into an actionable pricing tool? What margin should the company add to predicted costs, and how would you communicate the uncertainty bands to the sales team when they're bidding on new contracts?
- The cost distribution likely varies substantially across vehicle types, route types, and delivery priorities. Should you train a single model across all segments, or consider separate models for distinct operational profiles?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (distribution shape, log-normality, skewness), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to the pricing team: how should the predicted costs be used for dynamic pricing? Where is the model most and least reliable?

---

### Phase 3: The Ethical Crossroads

Carmen Reyes's analysis is straightforward: if `driver_experience_years` is used for route assignment, senior drivers will accumulate the performance records that justify their preferential treatment, while junior drivers will be trapped in a self-reinforcing cycle of difficult routes and poor metrics. Marco DeSilva's counter is equally clear: matching skill to difficulty is standard practice in every safety-critical industry.

**Guiding questions:**
- If driver experience improves model accuracy but its use for route assignment produces systematically different career outcomes for junior versus senior drivers, how would you assess whether the system creates inequitable outcomes? What specific metrics would you compute, and what patterns would you look for in the data to test Reyes's "caste system" hypothesis?
- Nina frames the dilemma: "a system that optimizes for the number versus a system that's fair to the people behind the number." Construct arguments for both positions. Is there a middle path — perhaps a mentorship pairing model, a rotation system, graduated route assignment, or a constrained optimization — that balances predictive accuracy with workforce equity?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position: Should Apex Logistics use driver experience years as a feature in its route assignment system? Defend your position with both analytical evidence from the data and ethical reasoning grounded in labor equity principles. If you propose a middle path, specify exactly how it would work in practice — vague compromises will not be accepted.

---

### Phase 4: The Board Room

It is early March. Nina faces Apex's CEO on Monday morning. If the system passes internal review, she presents to David Hargrove and the Ridgeline team on Friday.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the CEO (operationally focused, financially motivated) and, separately, a client logistics VP who has already been burned once (technically sophisticated, deeply skeptical). Prepare a single document that serves both: communicate (a) the root causes of the holiday season failures and the data evidence behind them, (b) what your models reveal about which shipments are most likely to fail and why, (c) your recommended dispatch prediction system and dynamic pricing approach, and (d) what the data *cannot* tell them. No jargon for the CEO. Full methodological credibility for the client. The best executive briefs accomplish both.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best operations analysts don't just answer the questions they're given — they find the questions nobody thought to ask. What did you discover in the data that is not covered by Phases 1–3? A vehicle-weather combination that fails at three times the fleet average? A route type where costs and on-time rates diverge in unexpected directions? A driver experience threshold below which performance degrades nonlinearly? A seasonal pattern in the entry errors that suggests a specific TMS software bug? A pricing anomaly that means Apex is losing money on 15% of its routes without knowing it? There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

## Data Resources

| Resource | Path |
|---|---|
| Delivery Dataset | `datasets/transportation/synthetic_transportation_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/transportation_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/transportation_tasks.md` |

Students should begin by loading the dataset and performing independent exploratory data analysis before engaging with the discussion questions. The data dictionary provides complete column definitions, data types, and valid value ranges.

---

## Exhibits

- **[Exhibit A](exhibits/exhibit_A.md)** — Letter from David Hargrove, VP of Logistics at Ridgeline Retail, formally notifying Apex Logistics of contract termination and conditions for reinstatement
- **[Exhibit B](exhibits/exhibit_B.md)** — Apex Logistics Operations Dashboard — Fleet Performance Snapshot

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Route That Broke the Contract." *From Data to Decisions*, Case 10. University of North Texas.
