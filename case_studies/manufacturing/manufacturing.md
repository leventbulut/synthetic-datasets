# The Tolerance Stack

## When Every Shift Tells a Different Story — Precision Dynamics and the Quality Collapse

---

**From Data to Decisions** | The Tolerance Stack — Manufacturing Analytics

**Data:** `datasets/manufacturing/synthetic_manufacturing_20250901.csv`
**Data Dictionary:** `documentation/data_dictionaries/manufacturing_dictionary.md`
**Suggested Tasks:** `documentation/suggested_tasks/manufacturing_tasks.md`

---

## I. Ninety Days

The email arrived at 6:47 on a Monday morning in early March, before Angela Torres had finished her first cup of coffee. It was from the quality compliance group at Northfield Automotive — Precision Dynamics' largest customer, a Tier 1 OEM whose drivetrain assemblies went into three of the five best-selling pickup trucks in North America. The subject line read: *FORMAL QUALITY NOTICE — Precision Dynamics LLC — Supplier Code 4417.* She opened it, read two paragraphs, and set the cup down.

Northfield's incoming inspection team had been tracking an upward trend in defect escapes on Precision Dynamics' automotive shipments. Over the previous two quarters, the rolling defect escape rate had climbed past their contractual threshold. The notice was professional but unambiguous *(see Exhibit A)*: if Precision Dynamics could not demonstrate a corrective action plan and drive the escape rate below 2% within ninety days, Northfield would initiate contract termination proceedings. The contract was worth $45 million annually — roughly a third of Precision Dynamics' total revenue.

Torres was the Director of Quality Engineering at Precision Dynamics, a multi-line manufacturer producing electronics assemblies, automotive components, consumer goods, and industrial parts across a 340,000-square-foot facility in the upper Midwest. She had held the role for four years and had inherited a quality system that was adequate for the company's mid-market positioning — until the company had started winning larger, more demanding customers like Northfield. The gap between "adequate" and "world-class" was now measured in defect escapes and contract penalties.

She forwarded the notice to the plant manager and the CFO, then walked down to the production floor. It was the end of the Night shift, and the Automotive line was running its last batches before the Day crew arrived. She stood at the end of the inspection station and watched a quality technician sort finished parts. The reject bin was not empty.

By 9 AM, Torres had pulled 400,000 production batch records from the Manufacturing Execution System — every batch run across all four product lines over nearly three years. Twenty-one columns of data: machine parameters, environmental conditions, operator metrics, maintenance logs, material quality scores, and quality outcomes. She loaded the first summary view and realized the Northfield problem was not the problem. It was a symptom.

Across all four product lines, quality was deteriorating — but unevenly. The defect rate on the Electronics line during the Night shift was nearly double the rate on the Consumer Goods line during the Day shift. The Automotive line showed the tightest quality overall, yet it was the one generating the customer complaint. The Industrial line, which ran the fewest batches, had the widest variance — some batches were pristine, others were scrap-heavy. The question was not whether quality was slipping. The question was why it was slipping differently everywhere.

---

## II. The MES and Its Ghosts

Torres assembled a small cross-functional team: herself, a process engineer named David Kwon, a data analyst named Priya Sharma from the finance group, and the IT systems administrator who managed the MES. Their first objective was to understand what the data could and could not tell them.

"The good news," Sharma said, pulling up a summary on the conference room screen *(see Exhibit B)*, "is that we have volume. Four hundred thousand batch records, twenty-one fields per record, spanning roughly thirty months of production. We have machine age, operator experience, environmental readings — temperature, humidity, vibration, power consumption — cycle times, defect and scrap rates, supplier quality scores, maintenance logs, and both a quality classification and a total production cost for every batch."

Torres nodded. "And the bad news?"

"The MES has its own quality problems."

Sharma walked them through what she had found in her preliminary review. Approximately 12,000 records — about 3% of the dataset — had missing values across several sensor fields: vibration level, temperature, humidity, power consumption, and defect rate. The missingness was not scattered randomly. It clustered in ways that suggested a systematic cause. Sharma suspected — but could not yet confirm — that the sensor readings dropped out when machines entered maintenance mode, and that the MES did not distinguish between "sensor reading is zero" and "sensor was not recording."

But the missing values were not the only concern. A second layer of problems was harder to see. Torres turned to the IT administrator. "Tell them about the machine age correction."

The administrator shifted uncomfortably. "About eighteen months ago, we noticed that some machine age entries were obviously wrong — values that didn't match our asset register. A few showed machines as being fifty or sixty years old when the facility itself was built less than thirty years ago. So we wrote a script to flag and correct them." He paused. "The script didn't work exactly as intended. It corrected some values that were already right, and it introduced a new set of entries that are plausible but wrong. We caught it and stopped the script, but the corrupted records are still in the system."

Kwon frowned. "How many?"

"We're not sure. The script ran on about twenty thousand records before we killed it. Some of those corrections were legitimate. Some weren't. There's no clean way to tell which is which without going back to the asset tags on the machines themselves."

Torres looked at Sharma. "What else?"

Sharma pulled up a histogram. "There are about 800 records — a fraction of a percent — with sensor values that are physically impossible. Temperatures above 200°C on production lines that operate between 30 and 120. Vibration readings of 30 to 80 millimeters per second on machines rated for a maximum of 15. Power consumption values five to ten times the rated capacity of the equipment. These look like sensor malfunctions or data transmission errors."

"And then there are the entry errors that aren't as dramatic," she continued. "Downtime entries of 500 to 1,500 minutes — that's eight to twenty-five hours of downtime in a single batch. Cycle times of 500 to 1,200 seconds per unit on processes that should run in 5 to 200 seconds. These aren't sensor failures. They look like someone entered minutes where the field expected seconds, or typed a shift-total where the field expected a batch-level number."

The team sat with this for a moment. The dataset was large enough to build powerful models. But the data carried scars — some from machines, some from software, some from people.

---

## III. Two Targets, Two Problems

Torres had two immediate needs, and they mapped to two different columns in the dataset.

**The quality problem** was existential. The `quality_level` field classified every batch as High, Medium, or Low quality based on post-production inspection. The distribution was stark: roughly 8 to 12% of batches earned a High classification, 15 to 20% were Medium, and the remaining 68 to 77% were Low. The skew was severe. If the team built a quality prediction model that simply guessed "Low" for every batch, it would be right most of the time — and completely useless. The real value was in identifying the conditions that produced High and Medium outcomes, and in catching Low-quality batches before they shipped.

Torres wanted a real-time quality prediction system — something that could take in the machine parameters, environmental readings, and operator data for a batch in progress and flag it as likely-Low before it reached final inspection. If they could catch quality problems upstream, they could intervene during production rather than sorting defective parts at the end of the line. That was the argument that might satisfy Northfield.

**The cost problem** was strategic. The CFO had been asking for months for a production cost model that could support shift scheduling and production planning decisions. The `production_cost` field captured total batch cost in dollars. The distribution was log-normal, centered around $2,400 but with a long right tail stretching from a few hundred dollars to $100,000 for complex, high-volume batches. Sharma noted that the log-normal shape meant standard linear regression on raw costs would be dragged around by the tail — the handful of $80,000 batches would dominate the error metrics and distort the model's behavior on the $1,500-to-$5,000 batches that constituted the daily reality of the plant.

The CFO's question was deceptively simple: *What does it cost to run an extra Night shift on the Electronics line versus adding a Day shift on Consumer Goods?* Answering it required untangling the effects of machine age, operator experience, batch size, environmental conditions, and product line on cost — and doing it with data that had the quality issues Sharma had catalogued.

---

## IV. The Shift Problem

Three weeks into the analysis, Kwon brought a finding to Torres that complicated everything.

"I've been looking at quality outcomes broken down by shift and operator experience," he said, laying out a grid of box plots on the conference table. "And the pattern is clear. Night shift batches have lower quality levels, higher defect rates, and higher scrap rates than Day or Evening shift batches. The gap is statistically significant and practically meaningful."

Torres had expected this. Night shifts were universally harder — fatigue, skeleton crews, fewer supervisors on the floor. But Kwon was not finished.

"The reason isn't just the shift itself," he continued. "It's who's working it. The Night shift operators have, on average, significantly less experience than the Day shift operators. Junior operators get assigned to nights. That's how the rotation has always worked — you start on nights and earn your way to days. The model sees `operator_experience` and `shift` as two of its strongest predictors of quality. And they're correlated, because the assignment policy links them."

Sharma had run the numbers both ways — models with and without operator experience and shift as features. Including them substantially improved the model's ability to predict Low-quality batches. The model was not just seeing noise. It was capturing a real operational pattern: less experienced operators, working in less supervised conditions, on equipment that might not have been optimally maintained, were producing lower-quality output.

Torres saw the problem immediately. "If we deploy this model on the shop floor, what happens?"

Kwon laid it out. "The model flags batches as high-risk when a junior operator is running a Night shift on an older machine. That's a legitimate quality signal — the data supports it. But the operators will see it differently. They'll see a system that brands them as a risk factor. The experienced Day shift operators will never trigger a flag. The junior Night shift operators will trigger one every time."

"And the union will see it as surveillance," Torres said quietly.

She was right. Two days later, Ray Dominguez, the local union steward, was in her office. He had heard about the analytics project from a line supervisor. "I want to be clear," Dominguez said, leaning forward in his chair. "If this company uses an algorithm to score my members' performance — if a machine decides that Carlos on nights is a quality risk and Jennifer on days isn't — there will be a grievance on your desk the same afternoon. We bargained evaluation criteria in the last contract. An algorithm wasn't one of them."

Torres tried to explain that the model was about process improvement, not performance management. Dominguez was not persuaded. "That's what they always say. Until someone uses the model's output in a disciplinary meeting. I've seen it happen at other plants. You build a 'training tool,' and six months later it's an 'accountability system.'"

The plant manager, Jim Hadley, had a different perspective. "We're not trying to punish anyone," he told Torres after Dominguez left. "But we can't pretend the data doesn't exist. If junior operators need more training, more supervision, or better shift conditions to produce quality output, then the model is telling us where to invest. Ignoring that signal doesn't help the operators — it just lets us keep assigning them to fail."

Torres was not sure either of them was wrong. The model was technically sound. Operator experience and shift assignment were real predictors of quality outcomes. But deploying a system that effectively scored operators by seniority and shift — even if the intent was training, not punishment — created risks that were not captured in any confusion matrix. The operators who triggered the most alerts would be the ones with the least power to change their circumstances. The system would be accurate. Whether it would be fair was a different question.

---

## V. The Presentation

By late spring, Torres had the outlines of a response to Northfield's quality notice, but the analytics work had surfaced questions that went beyond the automotive line. She was scheduled to present to the plant leadership team the following week. Northfield had also sent a quality auditor, Karen Lindstrom, who would sit in on the presentation to evaluate whether Precision Dynamics was taking the corrective action seriously.

Torres had data, models, and a team that had done rigorous work. What she did not have was consensus on the hardest question: how to use what the model had found about operators and shifts without crossing the line from process improvement into algorithmic performance management.

She opened the dataset one more time. Four hundred thousand batch records. Four hundred thousand production runs, each one representing a shift of someone's working life — a machine warming up, an operator calibrating tolerances, a batch of parts that would go into a truck or a circuit board or a household appliance. The numbers were in there, waiting to reveal whether the system was producing quality or merely producing volume. And somewhere in the gap between those two words lay the question of what the company owed to the people who stood at the machines every night, running the lines that nobody wanted to run, producing the output that the models judged most harshly.

She closed the laptop and went to the shop floor. The Night shift was starting.

---

## Your Assignment

You are a member of Angela Torres's cross-functional analytics team at Precision Dynamics. Using the facility's 400,000-record MES database, you will work through four phases — mirroring the real-world arc of a manufacturing analytics engagement: from data audit to boardroom presentation.

For companion analytical questions and additional modeling tasks, see the suggested task set in `documentation/suggested_tasks/manufacturing_tasks.md`.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Precision Dynamics' MES data is large and operationally rich — but it carries the scars of sensor malfunctions, a botched IT correction script, and the accumulated entry errors of a three-shift operation running around the clock. Your first task is to determine what you can trust, what you can't, and what you must handle with care.

**Guiding questions:**
- You have 400,000 records with 21 columns and approximately 12,000 missing values concentrated in sensor fields. Before looking at specific columns, what framework would you use to assess whether the missing data are MCAR, MAR, or MNAR? Why does this distinction matter for a manufacturing dataset where sensor readings may drop out during maintenance windows?
- The case describes three distinct categories of data quality problems: missing sensor readings (~3%), physically impossible sensor values (~0.2%), and plausible-but-wrong entry errors (~5%). Design a data quality audit strategy that addresses each category differently. What domain knowledge about manufacturing processes would you bring to bear?
- The IT administrator's correction script ran on approximately 20,000 records before being stopped. How would you approach identifying which "corrections" were legitimate and which introduced new errors? What does this tell you about the risks of automated data cleaning?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, physically impossible readings, distributional anomalies, and the artifacts of the IT correction script. Investigate whether the missingness is random or structured: does it correlate with shift, product line, machine age, or maintenance events? This report must convince both Torres's engineering team and Northfield's quality auditor that the data foundation is understood — scars and all.

---

### Phase 2: The Prediction Challenge

Precision Dynamics must build two systems — one for the shop floor, one for the CFO's office.

#### Part A — Batch Quality Classification

Northfield demands a corrective action plan. Torres wants to catch quality problems before they reach final inspection. Predict `quality_level` (High = 0 / Medium = 1 / Low = 2).

**Guiding questions:**
- The target has three classes with a heavily skewed distribution — the majority of batches are classified as Low. What challenges does this severe imbalance create for model training and evaluation? Propose at least two strategies for handling it, and explain why simply predicting "Low" for every batch is useless despite being frequently correct.
- In a manufacturing quality system, what is the cost of classifying a Low-quality batch as High (defect escape to the customer) versus classifying a High-quality batch as Low (unnecessary rework and scrap)? How would you encode this asymmetry into your evaluation framework?
- Which features are most predictive of quality level? Do machine parameters, environmental conditions, operator factors, or material quality scores dominate — and does the answer change by product line?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with manufacturing-appropriate metrics, and interpretation. Address the severe class imbalance and the asymmetric cost of misclassification — a defect that escapes to Northfield is not the same as an internal rework. Conclude with a recommendation: how should this model be deployed on the production floor for real-time quality monitoring?

#### Part B — Production Cost Regression

The CFO needs a cost model for shift scheduling and production planning. Predict `production_cost`.

**Guiding questions:**
- Production cost follows a log-normal distribution centered around $2,400 with a long right tail extending to $100,000. What does this distributional shape imply for your choice of regression model, error metric, and any necessary transformations?
- The CFO's question is deceptively simple: *What does it cost to run an extra Night shift on the Electronics line versus adding a Day shift on Consumer Goods?* What features in the dataset would you use to answer this, and how would you isolate the shift effect from confounding variables like operator experience and machine age?
- Which cost drivers are controllable (e.g., shift scheduling, maintenance frequency) versus structural (e.g., product line, batch size)? How does this distinction affect the practical value of your recommendations?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (log-normal shape, heavy right tail — investigate the cost outliers), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Distinguish between controllable and structural cost drivers. Conclude with a recommendation to the CFO: where can the plant reduce cost without compromising the quality improvements that Northfield demands?

---

### Phase 3: The Ethical Crossroads

The model shows that `operator_experience` and `shift` are strong predictors of batch quality. Night shift operators — who tend to be junior — produce lower-quality output. Torres wants to use the model for process improvement. The union sees algorithmic surveillance. The plant manager says ignoring the signal lets the company keep assigning junior operators to fail.

**Guiding questions:**
- Should Precision Dynamics deploy a quality prediction model that uses operator experience and shift assignment as features? Defend your position with both analytical and ethical reasoning. Consider: if these features are excluded, will the model simply capture the same signal through correlated variables like machine age, maintenance hours, and environmental conditions during night operations?
- Ray Dominguez argues that algorithmic quality scores will inevitably migrate from "training tools" to "accountability systems." Jim Hadley argues that ignoring the data means ignoring an opportunity to support junior operators. Is there a deployment framework — technical, organizational, or contractual — that genuinely prevents the first outcome while enabling the second? What would it look like in practice?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on whether and how operator-level features should be included in the quality prediction model. Defend your position with both analytical evidence from the data and ethical reasoning about labor relations, algorithmic accountability, and the power dynamics of shift work. Address the counterargument directly. If you propose a middle path, specify the technical and organizational safeguards that would make it work — not in theory, but on this shop floor, with this union, under this contract.

---

### Phase 4: The Board Room

It is late spring. Torres stands before the plant leadership team and Northfield's quality auditor, Karen Lindstrom. The $45 million contract — and the jobs that depend on it — hangs on this presentation.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the plant manager, the CFO, the union steward, and an external quality auditor from the customer. Communicate: (a) root causes of the quality deterioration across product lines and shifts, (b) the real-time quality prediction system's capabilities and validation results, (c) specific corrective actions — what changes on the shop floor starting next week, (d) how the model handles the operator experience question without crossing into performance surveillance. No jargon. No hedging. The auditor needs to trust the system, the union needs to trust the intent, and the CFO needs to see the cost case.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts do not just answer the questions they are given — they find questions nobody thought to ask. What did you discover in Precision Dynamics' data that is not covered by Phases 1–3? A product-line pattern hidden in the production dates, an unexpected interaction between environmental conditions and material quality, a machine-age threshold where quality falls off a cliff, or a finding that challenges the "Night shift problem" narrative itself. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

| Resource | Path |
|----------|------|
| Dataset | `datasets/manufacturing/synthetic_manufacturing_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/manufacturing_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/manufacturing_tasks.md` |

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Tolerance Stack." *From Data to Decisions*, Case 6. University of North Texas.
