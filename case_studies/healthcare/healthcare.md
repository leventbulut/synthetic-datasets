# Thirty Days

**A Data Science Case Study in Hospital Readmission Prediction**

**From Data to Decisions** | Thirty Days to Avoid a $4.2M Penalty — Healthcare Analytics

---

> **Data Resources**
>
> - Dataset: `datasets/healthcare/synthetic_healthcare_20250901.csv`
> - Data Dictionary: `documentation/data_dictionaries/healthcare_dictionary.md`
> - Suggested Tasks: `documentation/suggested_tasks/healthcare_tasks.md`
> - Exhibit A: CMS Penalty Notice — `case_studies/healthcare/exhibits/exhibit_A.md`
> - Exhibit B: Hospital Operational Dashboard — `case_studies/healthcare/exhibits/exhibit_B.md`

---

## I. The Letter

On a gray Monday morning in January, Dr. James Okafor set his coffee on the desk and opened the envelope from the Centers for Medicare & Medicaid Services. He already knew what it would say — word had been circulating among the quality officers at neighboring hospitals for weeks — but seeing the number in print still stung. Lakeview Regional Medical Center's 30-day readmission rate had exceeded the national benchmark for the third consecutive measurement period. Effective the following October, Lakeview would face a 3% reduction in Medicare reimbursements. For a 450-bed community hospital where Medicare patients accounted for the majority of inpatient revenue, that penalty translated to approximately $4.2 million per year.

James read the letter twice, folded it into his portfolio, and walked to the office of the Chief Financial Officer.

"We knew this was coming," said CFO Maria Santos, not looking up from her monitor. "The question is whether we can fix it in time for the next measurement window."

"That depends," James said, "on whether we can figure out which patients are coming back — and why."

Maria turned in her chair. "You've got the data?"

"Half a million patient records from the last two and a half years. Admissions, vitals, labs, insurance, costs — everything the EHR captures." James paused. "But I've got some concerns about the data itself."

---

## II. Lakeview Regional Medical Center

Lakeview Regional Medical Center served a mixed suburban-rural catchment area of roughly 600,000 residents. With 450 licensed beds spread across six departments, the hospital handled everything from routine elective surgeries to Level II trauma. Its patient population was economically diverse: a substantial share of patients carried Medicare or Medicaid, while a meaningful number were uninsured or self-pay (see Exhibit B).

The hospital's six departments reflected the breadth of its mission. Pediatrics handled the largest share of admissions — over 128,000 of the 500,000 records in the extract — followed by the Intensive Care Unit with more than 91,000 encounters. General Medicine contributed nearly 90,000 admissions, while the Emergency Department logged approximately 81,000. Cardiology and Surgery rounded out the census at roughly 60,000 and 50,000 admissions respectively.

Admission pathways were split across four categories. Elective admissions represented the largest group at 158,274, followed closely by urgent admissions at 148,828. Trauma cases numbered 96,719, and emergency admissions accounted for 96,179. The average length of stay across all departments was 5.8 days, though James knew that average concealed enormous variation — a simple appendectomy bore no resemblance to a complicated cardiac recovery.

Financially, the mean total cost per patient encounter was $10,997, with a median of $9,987 and a standard deviation of $4,303. That gap between the mean and median told James something he already suspected: a long right tail of expensive cases was pulling the average upward. The question Maria kept asking was deceptively simple: *which patients cost us the most, and can we see them coming?*

---

## III. The Readmission Problem

The CMS Hospital Readmissions Reduction Program penalizes hospitals whose 30-day readmission rates for specific conditions exceed expected levels. The policy rationale is straightforward: readmissions within 30 days of discharge often signal a failure in care quality, discharge planning, or post-acute coordination. Hospitals that fail to reduce preventable readmissions absorb a financial penalty on *all* Medicare discharges — not just the readmitted patients.

Lakeview's EHR system captured readmission risk as a three-tier classification. Of the 500,000 patient records James had extracted, 263,357 patients (52.7%) were classified as low risk. Another 129,842 (26.0%) fell into the medium-risk category. And 106,801 — over one in five patients, at 21.4% — were classified as high risk.

"One in five," James repeated to his analytics team during their first working session. "If we can move even a fraction of those high-risk patients into effective post-discharge programs — transitional care, telehealth follow-ups, pharmacy reconciliation — we might be able to bend the curve."

His lead analyst, Priya Chandrasekaran, was less optimistic. "We can build a predictive model," she said. "But the question isn't whether we can predict readmission risk. The question is whether we can predict it *well enough* to act on, early enough to matter, with data clean enough to trust."

---

## IV. The Data Question

Priya's caution was well-founded. Over the prior eighteen months, Lakeview had weathered a nursing staffing crisis that hit the Emergency Department hardest. Travel nurses, unfamiliar with the hospital's EHR workflows, had been inconsistent in their charting. Karen Liu, the nursing informaticist who had managed the crisis, gave James a candid assessment.

"We did the best we could," Karen said. "But when you're running an ED at 140% capacity with half the staff on 60-day travel contracts, documentation takes a hit. Vital signs, lab orders, triage notes — it was triage in every sense of the word."

The dataset James had pulled reflected this reality. Across 500,000 records and 21 columns, there were 14,996 missing values — not a staggering number in percentage terms, but their distribution mattered more than their count. The missingness was concentrated in specific clinical fields rather than spread uniformly across the dataset.

"The pattern of what's missing may be as important as the values themselves," Priya told the team. "If the gaps are random, we can handle them statistically. If they're *not* random — if they correlate with patient acuity, department, or time period — then imputation could introduce systematic bias into the model."

James nodded. Beyond missing values, there were other concerns. Karen had flagged that during the staffing crisis, some charted values appeared implausible — likely data-entry errors made under time pressure. The data dictionary noted that approximately 5% of records might contain entry errors, and about 0.2% contained genuine outliers.

"So our first job," James said, "isn't building models. It's understanding what we're working with."

---

## V. Two Models, Two Questions

By mid-January, James had secured a six-month runway from the hospital's executive committee. The mandate was clear: build an analytical foundation for a readmission reduction initiative that could demonstrate results before the next CMS measurement window.

The work naturally divided into two tracks.

**Track One: Classification.** CMS needed a readmission risk model that could stratify patients at discharge into low, medium, and high risk categories. The care coordination team — nurses, social workers, pharmacists — had limited bandwidth. They could not follow up with every discharged patient. The model needed to identify which patients would benefit most from intensive post-discharge interventions. The target variable was `readmission_risk`, a three-class problem.

Priya laid out the modeling considerations. "With 52.7% of patients in the low-risk category and only 21.4% in high-risk, we have a moderate class imbalance. Not extreme, but enough that a naïve model could achieve decent overall accuracy while performing poorly on the class that matters most." She looked at James. "We need to decide: is missing a high-risk patient worse than flagging a low-risk one for unnecessary follow-up?"

The answer seemed obvious — of course missing a high-risk patient was worse. But James had sat through enough budget meetings to know that false positives had costs too. Every unnecessary home health visit, every redundant telehealth call, consumed resources that could have gone to a patient who truly needed them.

**Track Two: Regression.** CFO Maria Santos had a parallel question that was less about clinical outcomes and more about financial sustainability. "I need to know which patients are going to cost us the most," she told James. "Not after the fact — before the fact. If we can predict `total_cost` at or near admission, we can staff appropriately, negotiate with insurers more effectively, and flag cases that might need utilization review."

The cost data told an interesting story even before modeling began. With a mean of $10,997 and a standard deviation of $4,303, total cost varied substantially across the patient population. The gap between the mean and the $9,987 median suggested a right-skewed distribution. Understanding the drivers of that skew — which combinations of diagnosis, acuity, comorbidity, and length of stay pushed costs into the upper tail — would be as valuable as the point predictions themselves.

---

## VI. The Insurance Question

It was during the third week of analysis that Priya brought James a finding that stopped the project cold for 48 hours.

"I've been profiling readmission risk across patient subgroups," she said, placing a chart on his desk. "Age, diagnosis, department, comorbidities — the usual suspects. But look at this." She pointed to the breakdown by insurance type.

The pattern was stark. Patients classified as Self-Pay — those without insurance coverage — appeared to have a meaningfully different readmission risk profile than privately insured patients. The relationship held even after controlling for clinical factors.

James stared at the chart. "If we include insurance type in the model, it improves prediction."

"Almost certainly," Priya said. "Insurance status is correlated with social determinants of health — access to follow-up care, medication affordability, transportation, housing stability. From a purely predictive standpoint, it's a useful feature."

"And from an ethical standpoint?"

Priya set the chart down. "If we build a model that flags uninsured patients for extra follow-up, we're essentially targeting people based on socioeconomic status. You could frame it as *helping* them — giving them more resources. Or you could frame it as *profiling* them — treating them differently because of their financial situation."

The ambiguity was genuine, and James knew the hospital board would see it from both sides. Patient advocates would argue that directing more resources toward vulnerable populations was exactly what equity-focused healthcare demanded. Legal counsel might counter that using insurance status as a predictive feature could expose the hospital to disparate impact claims. And ethicists would ask whether the model's recommendations, even if well-intentioned, might create a self-fulfilling prophecy — labeling uninsured patients as high-risk in ways that altered their care trajectory.

"There's another angle," Priya added. "If we *exclude* insurance type and the model performs worse, we might miss high-risk patients who happen to be uninsured. Is that more ethical? We'd be protecting their privacy at the cost of their health outcomes."

James didn't have an answer. He suspected there wasn't one — at least not one that a predictive model could provide.

---

## VII. Preparing for the Board

By late February, the analytics team had enough preliminary work to structure a board presentation. James outlined the agenda with Maria and the Chief Medical Officer, Dr. Susan Park.

The presentation would need to cover three areas:

First, **data quality and trustworthiness.** Before any model results, the board needed to understand what the data could and could not support. The 14,996 missing values, the documentation inconsistencies from the staffing crisis, the entry errors — all of these affected how much confidence the board should place in model outputs. James wanted the board to understand that a model built on flawed data would produce flawed predictions, no matter how sophisticated the algorithm.

Second, **predictive models and their limitations.** The readmission risk classifier and the cost regression model would be presented side by side, with honest assessments of performance. James wanted to avoid the trap he'd seen at other hospitals: presenting a model's accuracy on training data as if it guaranteed real-world performance. He planned to show the board what the models got right, what they got wrong, and where uncertainty was highest.

Third, **the implementation question.** A model sitting in a Jupyter notebook saved no patients and avoided no penalties. The board needed to see a concrete plan for embedding predictive scores into clinical workflows — at discharge, in care coordination meetings, in utilization review. That plan required IT investment, staff training, and workflow redesign. It also required a clear policy on the insurance-type question that Priya had raised.

"The $4.2 million penalty is the burning platform," Maria said. "But the board will want to know: how much does it cost to build the parachute?"

---

## Your Assignment

You have been retained as an external analytics consultant supporting Dr. Okafor's initiative. Using Lakeview Regional Medical Center's 500,000-record patient dataset, you will work through four phases — mirroring the real-world arc of a clinical analytics engagement: from data audit to board presentation.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Lakeview's dataset carries the scars of an eighteen-month staffing crisis. Travel nurses with inconsistent charting, overloaded departments, and competing documentation priorities have left marks in the data. Your first task is to determine how deep those marks go.

**Guiding questions:**
- Where are the data quality issues concentrated — in specific departments, patient acuity levels, or time periods? Do the missingness patterns align with the staffing crisis narrative?
- Under what circumstances would you impute missing values versus exclude records? How do your choices affect downstream modeling?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, implausible vitals, entry errors, and distributional anomalies. For each issue, state what you found, quantify its scope, and recommend a handling strategy. This report should answer Dr. Okafor's foundational question: *Is the data trustworthy enough to build clinical models on?*

---

### Phase 2: The Prediction Challenge

Lakeview faces a $4.2 million penalty and a board that wants answers.

#### Part A — Readmission Risk Classification

The CMS penalty targets 30-day readmissions. Predict `readmission_risk` (Low / Medium / High).

**Guiding questions:**
- Given the class distribution (52.7% / 26.0% / 21.4%), what metric should you optimize — and why? What is the relative cost of a false negative (missing a high-risk patient) versus a false positive (flagging a low-risk patient)?
- Identify the top features driving readmission risk. Which are actionable (the hospital can intervene) and which are informational (useful for stratification but not modifiable)?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with clinically appropriate metrics, and interpretation. Address the class distribution and asymmetric cost of misclassification explicitly. Conclude with a clear recommendation: which features should the care coordination team monitor, and how would you embed this model into discharge workflows?

#### Part B — Total Cost Regression

The CFO needs to understand what drives patient costs. Predict `total_cost`.

**Guiding questions:**
- The mean cost ($10,997) exceeds the median ($9,987) by roughly $1,000. Investigate the right tail of the cost distribution. What patient profiles are associated with extreme costs?
- How should the hospital use cost predictions for staffing, utilization review, and insurer negotiations? Where should the CFO trust the model, and where should she be skeptical?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (mean $10,997, median $9,987 — investigate the right tail), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to CFO Maria Santos: how should cost predictions inform financial planning? Characterize the error distribution — where does the model perform well, and where does it struggle?

---

### Phase 3: The Ethical Crossroads

Priya's analysis revealed that insurance type — particularly Self-Pay status — is a meaningful predictor of readmission risk. Including it improves accuracy. Excluding it may cause high-risk uninsured patients to be missed.

**Guiding questions:**
- Should the readmission risk model include `insurance_type` as a predictor? Construct arguments for both positions. What alternative approaches might capture the predictive signal without using it directly?
- If Lakeview implements a readmission risk score in clinical workflows, what safeguards should be in place to prevent the model from reinforcing existing disparities in care?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on the insurance-type question. Defend your position with both analytical evidence from the data and ethical reasoning. Address the counterargument directly. If you propose an alternative approach (e.g., proxy variables, separate models, post-hoc adjustment), specify exactly how it would work and what trade-offs it introduces.

---

### Phase 4: The Board Room

It is late February. Dr. Okafor stands before Lakeview's hospital board. The $4.2 million penalty is the burning platform.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the Chief Medical Officer, the CFO, two community board members, and a patient advocate. Communicate: (a) the scope of the readmission problem, (b) what your models reveal about which patients are at highest risk and what drives cost, (c) your recommended readmission reduction strategy with projected impact, and (d) the data limitations and model uncertainties the board should understand. Maria Santos will ask: *"How much does it cost to build the parachute?"* Be ready.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in Lakeview's data that is not covered by Phases 1–3? A departmental pattern that warrants investigation, an unexpected interaction between clinical variables, a time-based trend the staffing crisis doesn't fully explain, or a patient subgroup that defies the model's assumptions. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2025 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2025). "Thirty Days." *From Data to Decisions*, Case 2. University of North Texas.
