# The Missing Signal

## BrightPath Community Mental Health Network and the Depression Screening Challenge

---

**From Data to Decisions** | The Missing Signal in Patient Recovery — Mental Health Analytics

**Data:** `datasets/depression/synthetic_depression_20250901.csv`
**Data Dictionary:** `documentation/data_dictionaries/depression_dictionary.md`
**Suggested Tasks:** `documentation/suggested_tasks/depression_tasks.md`

---

## I. The Dashboard That Lied

On the morning of March 3, Dr. Lena Vasquez stared at two charts projected on the screen of her corner office in BrightPath's downtown administrative hub. The first showed average PHQ-9 scores across the network's twelve clinics, plotted monthly for the past two years. The line was trending down — from a network-wide average of 12.1 eighteen months earlier to something closer to 10 by the most recent quarter. By any standard clinical interpretation, BrightPath was moving its patient population from solidly "moderate" depression toward the lower boundary of that range. Progress.

The second chart told a different story. Treatment dropout rates — patients who failed to return for three or more consecutive scheduled visits — had climbed from 18% to 26% over the same period. The improvement in average scores, Vasquez realized, might be an artifact. If the sickest patients were the ones leaving, the averages would improve even if no individual patient was getting better.

"We're getting better at treating patients who stay," she said to Marcus Chen, BrightPath's Director of Analytics, who sat across the conference table with his laptop open. "But we're losing the ones who need us most."

Chen nodded. He had been running preliminary analyses on the network's screening database for the past two weeks, ever since the state Medicaid office had sent its formal notice *(see Exhibit A)*. The stakes were clear: BrightPath's Medicaid waiver renewal, which funded roughly 60% of the network's operating budget, now required demonstrable outcome improvement and a validated predictive triage system by the upcoming September review deadline. Six months.

"The data we have is substantial," Chen said, pulling up a summary on the wall monitor *(see Exhibit B)*. "We're looking at 400,000 patient screening records across all twelve clinics, covering approximately thirty months of intake records. Thirty-two data fields per patient — demographics, clinical history, validated screening instruments, lifestyle factors, social determinants, treatment engagement."

Vasquez leaned forward. "And the data quality?"

Chen hesitated. "That's where it gets complicated."

---

## II. The BrightPath Network

BrightPath Community Mental Health Network operated twelve clinics across a mid-sized metropolitan area and its surrounding counties. Founded over fifteen years ago as a single community counseling center, BrightPath had grown through a series of state grants and Medicaid contracts into the region's largest provider of outpatient mental health services. The network served approximately 45,000 unique patients per year, with depression and anxiety disorders accounting for the majority of diagnoses.

The twelve clinics ranged from a 40-therapist urban flagship to rural satellite offices staffed by two or three clinicians. Each clinic had, over the years, developed its own intake procedures, screening workflows, and documentation habits. Some used paper intake forms that were later transcribed into the electronic medical record (EMR); others had patients complete digital screeners on tablets in the waiting room. Three clinics had briefly experimented with phone-based screening for follow-up appointments before abandoning the practice due to low completion rates.

The previous summer, BrightPath had migrated from its legacy EMR system — a patchwork of spreadsheets and a decade-old clinical platform — to a modern cloud-based system. The migration had been technically successful, but the transition period had introduced gaps. Data fields that had been mandatory in the old system were optional in the new one. Some clinics had retroactively entered historical records; others had not. The result was a dataset that was large and rich, but carried the scars of institutional change.

The patient population reflected the diversity of the communities BrightPath served. Employment statuses ranged widely: of the 400,000 records in the screening database, 101,919 patients were employed full-time, 90,616 were unemployed, 79,561 worked part-time, 69,933 were retired, and 57,971 were students. Among employed patients, occupations spanned dozens of sectors — from business operations and sales to construction, education, healthcare support, and food preparation. Annual household income, when recorded, varied from below the poverty line to upper-middle class.

---

## III. The State Mandate

The letter from the State Bureau of Behavioral Health Services arrived on February 14. It was not unexpected — the Medicaid waiver that funded BrightPath's core operations had always required periodic renewal — but the new requirements were significantly more demanding than in previous cycles *(see Exhibit A)*.

The Bureau now required participating provider networks to demonstrate three capabilities:

First, a validated **severity classification system** that could assign incoming patients to one of three care tiers — None/Mild, Moderate, or Severe — based on screening data collected at intake. The state wanted evidence that the model could accurately classify patients into these categories, with particular attention to sensitivity for severe cases.

Second, a **predictive recovery model** that could estimate a patient's likely treatment trajectory, enabling early identification of patients at risk for poor outcomes or treatment disengagement.

Third, a **quality improvement plan** that connected the predictive analytics to concrete clinical workflows — how would the models actually change what happened in the exam room?

"The classification piece maps directly to our existing depression severity labels," Chen explained to Vasquez. "We have a three-level target variable in the dataset: None/Mild, Moderate, and Severe. The distribution is uneven — about 52.7% of patients are classified as None/Mild, 19.0% as Moderate, and 28.2% as Severe. That imbalance is something we'll need to handle carefully."

Vasquez frowned. "More than a quarter of our patients are classified as Severe?"

"That's consistent with our role as a safety-net provider," Chen said. "We're not seeing the worried-well. We're seeing people who are already in crisis, or close to it. Our average PHQ-9 across the entire database is 10.3, which puts us right in the moderate depression range. Average GAD-7 is 7.2 — mild to moderate anxiety. These aren't population screening numbers. These are the scores of people who sought help because they were struggling."

The recovery score was more nuanced. BrightPath's clinical team had developed a composite metric that combined treatment response indicators — symptom reduction, functional improvement, sustained engagement — into a single score on a 5-to-100 scale. The mean recovery score across all 400,000 records was 76.3, but the median was 85.4, suggesting a left skew: most patients showed reasonable recovery, but a long tail of patients showed very poor treatment response. It was this tail that worried Vasquez most.

---

## IV. The Data Problem

Marcus Chen had spent two weeks with the dataset before the meeting with Vasquez, and he had assembled a preliminary assessment. The 400,000 records contained 32 columns spanning patient demographics, clinical history, validated screening instruments (PHQ-9 and GAD-7), lifestyle and behavioral measures, social factors, treatment engagement, and two target variables.

The good news: the dataset was large enough for rigorous modeling, and the feature space was clinically meaningful. Every variable in the dataset had a clear relationship to the depression literature. Screening instruments were validated. Treatment data was timestamped.

The bad news: the EMR migration had left marks.

Approximately 12,000 values were missing across the dataset — roughly 3% of all entries. But Chen suspected the missingness was not random. Certain fields seemed more likely to be absent in records from certain time periods, certain clinics, or certain patient populations. Understanding the pattern of missingness would be essential before any imputation strategy could be justified.

Beyond missing data, Chen had flagged other concerns during his initial exploration. Some records contained values that seemed clinically implausible — the kind of entries that happen when a tired intake coordinator transposes digits, misreads a form, or when a patient misunderstands a screening question. These were not common — perhaps less than one percent of records — but in a dataset of 400,000, even a small percentage meant thousands of potentially misleading observations.

"The thing that keeps me up at night," Chen told Vasquez, "is what we might be missing in the data that *looks* clean. Some of these values are technically valid — they fall within expected ranges — but they don't make clinical sense when you look at the patient's full profile. A data quality audit has to go beyond just checking for nulls and out-of-range values."

Vasquez nodded. She had seen this before. In her previous role as a clinical researcher at a university hospital, she had published a paper on how EMR data quality affected depression outcome studies. The irony of now facing the same challenge in her own network was not lost on her.

---

## V. The Occupation Question

Three weeks into the analysis, Chen brought a finding to Vasquez that complicated everything.

"I've been looking at recovery scores and severity distributions broken down by occupation," he said, spreading a series of visualizations across the conference table. "And there's a clear pattern. Patients in certain occupational categories have measurably worse outcomes — higher severity classifications, lower recovery scores, shorter treatment duration before dropout."

He paused. "The occupations aren't surprising, clinically. They're jobs characterized by high emotional labor, irregular schedules, low autonomy, and economic insecurity. But the signal is strong enough that including occupation as a feature in our models would meaningfully improve predictive accuracy."

Vasquez immediately saw the problem. "If we flag patients by job title, we're essentially profiling. A food service worker walks in the door and the model says 'high risk' before they've answered a single clinical question. That doesn't feel right."

"But if we *don't* flag them," Chen countered, "they fall through the same cracks they've always fallen through. These are the patients most likely to drop out of treatment. If we can identify them early, we can offer proactive outreach — more flexible scheduling, same-day appointments, peer support navigators. The clinical rationale is sound."

Vasquez stood and walked to the window. The BrightPath flagship clinic was visible two blocks away, its waiting room likely full at this hour. "There's a difference between identifying a vulnerable population for *support* and identifying them for *surveillance*," she said. "The model doesn't know which one we're doing. And once the state has the model, we don't control how it's used."

The dataset contained detailed occupation data for employed patients, spanning categories including Business Operations (20,927 patients), Sales (20,838), Management (20,788), Education (20,777), Construction (14,465), Architecture and Engineering (14,260), Sciences (14,172), Food Preparation (11,219), Office and Administrative (11,186), Personal Care (11,119), Healthcare Support (10,865), and Social Services (10,864). The variation in outcomes across these categories was not trivial.

Chen had run the numbers both ways — models with and without occupation features. The improvement in predictive accuracy was modest but statistically significant. More importantly, the model's ability to identify patients at risk for treatment dropout improved meaningfully when occupation was included.

"We have to decide before September," Vasquez said quietly. "And whatever we decide, we have to be able to defend it to the state review board."

---

## VI. The Path Forward

By mid-April, Vasquez and Chen had assembled a small analytics team — two data scientists, a clinical informaticist, and a community health equity specialist — to build BrightPath's response to the state mandate. They had six months, a 400,000-record dataset with known quality issues, and a set of questions that were as much ethical as they were technical.

The team's immediate priorities were clear:

**Data Quality.** Before any model could be trusted, the dataset needed a thorough audit. The 12,000 missing values were a starting point, but the team needed to investigate patterns of missingness, identify implausible values, and develop a cleaning and imputation strategy that could withstand scrutiny from both the state review board and BrightPath's clinical leadership. The strategy needed to be documented, justified, and reproducible.

**Severity Classification.** The state required a model that could classify patients into three severity tiers. With 52.7% of patients in the None/Mild category, 19.0% in Moderate, and 28.2% in Severe, the team needed to think carefully about class imbalance, the clinical cost of misclassification, and how to evaluate model performance in a context where missing a Severe case had life-or-death implications.

**Recovery Prediction.** The recovery score model would serve a different purpose — not triage, but early warning. With a mean of 76.3 and a left-skewed distribution, the team needed to understand what drove poor recovery outcomes and whether those drivers were modifiable. The gap between mean and median suggested that a substantial minority of patients were doing very poorly, and the model needed to find them.

**The Occupation Decision.** The team was split. The data scientists argued that excluding informative features was a form of willful blindness — that the model would simply find proxies for occupation through correlated variables like income, work hours, and sleep patterns, making the exclusion cosmetically clean but analytically dishonest. The equity specialist argued that including occupation explicitly would codify structural disadvantage into an algorithmic system, potentially creating a two-tiered care model where patients were judged by their job before their symptoms. The clinical informaticist noted that the model was only as ethical as the intervention it triggered — and that the right answer depended on what BrightPath would *do* with the predictions.

Vasquez had scheduled the state review board presentation for September 15. The team had data, talent, and institutional support. What they lacked was clarity — about the data, about the models, and about the line between prediction and prejudice.

She opened the dataset one more time. Four hundred thousand records. Four hundred thousand people who had walked through a BrightPath door looking for help. The numbers were in there, somewhere, waiting to reveal whether the system was working — or whether it was simply getting better at not seeing the people it was failing.

---

## Your Assignment

You are a member of BrightPath's newly assembled analytics team. Using the network's 400,000-record screening database, you will work through four phases — mirroring the real-world arc of a clinical analytics engagement: from data audit to state review board presentation.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

BrightPath's dataset is large and clinically rich — but it carries the scars of an EMR migration, twelve clinics with different documentation habits, and a patient population in crisis. Your first task is to determine what you can trust, what you can't, and what you must handle with care.

**Guiding questions:**
- You have 400,000 records with 32 columns and approximately 12,000 missing values. Before looking at specific columns, what framework would you use to assess whether the missing data are MCAR, MAR, or MNAR? Why does this distinction matter for a clinical dataset?
- Chen mentions that some records contain values that are "technically valid" but "don't make clinical sense." Design a data quality audit strategy that goes beyond null checks and range validation. What domain knowledge would you bring to bear?
- The EMR migration the previous summer is described as a source of data quality issues. How would you use the `screening_date` field to investigate whether data quality varies by time period? What visualization would you create?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, clinically implausible entries, distributional anomalies, and potential artifacts of the EMR migration. Investigate whether the missingness is random or structured: does it correlate with time period, clinic, patient demographics, or clinical severity? This report must convince both Chen's analytics team and the state review board that the data foundation is understood — warts and all.

---

### Phase 2: The Prediction Challenge

BrightPath must build two predictive systems for the state mandate — one for triage, one for early warning.

#### Part A — Depression Severity Classification

The state requires a validated severity classification system. Predict `depression_severity` (None/Mild / Moderate / Severe).

**Guiding questions:**
- The target has three classes with an uneven distribution (52.7% / 19.0% / 28.2%). What challenges does this create for model training and evaluation? Propose at least two strategies for addressing the imbalance.
- In a clinical triage system, what is the cost of classifying a Severe patient as None/Mild versus classifying a None/Mild patient as Severe? How would you encode this asymmetry into your evaluation framework? What metric(s) would you prioritize over simple accuracy?
- Which features are most predictive? Are there any that are surprisingly uninformative, or surprisingly powerful?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with clinically appropriate metrics, and interpretation. Address the class distribution and the life-or-death asymmetry of misclassification — missing a Severe patient is not the same as over-triaging a Mild one. Conclude with a recommendation: how should BrightPath's intake coordinators use this model at the point of first contact?

#### Part B — Recovery Score Regression

The state requires a predictive recovery model to identify patients at risk for poor outcomes. Predict `recovery_score`.

**Guiding questions:**
- The recovery score has a mean of 76.3 and a median of 85.4. What does this distributional shape tell you about the patient population? How would this affect your choice of regression model and error metric?
- Which factors are most strongly associated with poor recovery outcomes? Are these factors modifiable (e.g., treatment engagement) or fixed (e.g., demographics)?
- Chen's team wants to identify patients at risk for treatment dropout *before* they disengage. How would you use your recovery prediction model for this purpose? What threshold would you set, and how would you communicate the uncertainty to clinicians?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (mean 76.3, median 85.4 — investigate the left tail of poor responders), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Distinguish between modifiable and non-modifiable factors. Conclude with a recommendation to Dr. Vasquez: which patients should receive proactive outreach to prevent treatment dropout, and what does that outreach look like?

---

### Phase 3: The Ethical Crossroads

Chen's analysis revealed that occupation is a meaningful predictor of depression severity and recovery outcomes. Including it improves the model's ability to identify patients at risk for treatment dropout. Vasquez sees a line being crossed.

**Guiding questions:**
- Should BrightPath include occupation as a model feature? Defend your position with both analytical and ethical reasoning. Consider: what happens if occupation is excluded but the model captures its effect through correlated variables like income, work hours, and sleep patterns?
- The equity specialist argues that including occupation "codifies structural disadvantage." The data scientists argue that excluding it is "willful blindness." Is there a middle path — a way to use occupational information to *improve* equity rather than *reinforce* inequality? What would that system look like in practice?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on the occupation question. Defend your position with both analytical evidence from the data and ethical reasoning. Address the counterargument directly. If you propose a middle path — using occupation to *improve* equity rather than *reinforce* inequality — specify exactly how that system would work in practice.

---

### Phase 4: The Board Room

It is September 15. Vasquez stands before the state Medicaid review board. BrightPath's waiver renewal — and 60% of its operating budget — depends on this presentation.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes a Deputy Director of Behavioral Health, a clinical psychologist, a health actuary, an academic researcher, and a patient rights advocate. Communicate: (a) the predictive triage system's capabilities and validation results, (b) how it integrates into clinical workflow across 12 clinics with varying intake processes, (c) how BrightPath will monitor for bias and unintended consequences, and (d) what the data reveals about the "missing signal" — why average scores improved while dropout rates climbed. No jargon. No hedging. The board needs to trust both the system and the people behind it.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in BrightPath's data that is not covered by Phases 1–3? A clinic-level pattern hidden in the screening dates, an unexpected relationship between lifestyle variables and recovery, a subpopulation that the models consistently misjudge, or a finding that challenges the "missing signal" narrative itself. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Missing Signal." *From Data to Decisions*, Case 3. University of North Texas.
