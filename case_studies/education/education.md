# The Label Maker

## Lakeview Unified School District and the College Readiness Crisis

---

**From Data to Decisions** | When Prediction Becomes Prophecy — Education Analytics

**Data:** `datasets/education/synthetic_education_20250901.csv`
**Data Dictionary:** `documentation/data_dictionaries/education_dictionary.md`
**Suggested Tasks:** `documentation/suggested_tasks/education_tasks.md`

---

## I. Three Hundred Thousand Stories

The spreadsheet had been open on Dr. Carmen Reyes's monitor since six that morning. Three hundred thousand rows. Twenty-two columns. Each row a student — a name reduced to an ID, a life compressed into numbers. GPA. SAT score. Attendance rate. Family income. She scrolled past the first ten thousand rows before stopping, not because she had found what she was looking for, but because she realized she didn't yet know what she was looking for.

Carmen was eighteen months into her tenure as Chief Data Officer for Lakeview Unified School District, a sprawling suburban system that operated forty-seven schools — public, charter, and private — across three counties. She had been hired to modernize the district's analytics infrastructure, a mandate that had sounded exciting in the interview and had since revealed itself to be a euphemism for cleaning up decades of fragmented record-keeping. The previous summer's migration from a legacy Student Information System to a cloud-based platform had been, in the language of the IT department, "substantially complete." In the language of anyone who had to work with the data, it had been a controlled demolition.

The reason Carmen was at her desk before dawn was a memo *(see Exhibit A)*. Superintendent Patricia Okonkwo had sent it to the school board the previous Friday afternoon — the timing deliberate, Carmen suspected, to ensure maximum weekend anxiety among board members. The memo was blunt: Lakeview's college enrollment rate had dropped eight percentage points over the past three years. The decline cut across school types and geographies. It was not concentrated in any single feeder pattern or demographic subgroup. It was systemic.

The superintendent's response was a $2.4 million "College Readiness Initiative," and the centerpiece of that initiative was an early-warning system — a predictive model that could identify students at risk of falling behind before junior year, when, as Okonkwo put it, "the window for meaningful intervention has already closed." The data for that model was sitting on Carmen's screen. Three hundred thousand student records pulled from the SIS, spanning roughly thirty months of enrollment data across the district.

Carmen had spent the first two weeks running summary statistics and building exploratory visualizations *(see Exhibit B)*. The dataset was rich: academic metrics — GPA, SAT scores, AP courses, attendance — alongside study habits, school environment variables, family background, and well-being indicators. The district had invested in a holistic student record, capturing everything from weekly study hours and library visits to sleep patterns and self-reported stress levels. It was, on paper, exactly the kind of dataset that a modern early-warning system required.

On paper.

---

## II. The Scars of Migration

Carmen's analytics team consisted of three people: Malik Torres, a former school psychologist who had retrained in data science; Priya Anand, a statistician on loan from the county education office; and James Whitfield, a data engineer who had survived the SIS migration and bore the psychic scars to prove it.

It was Whitfield who first raised the alarm, two days into the exploratory analysis.

"The GPAs don't make sense," he said, turning his laptop toward Carmen during their morning standup. He had filtered for records where the cumulative GPA exceeded 4.0 — the theoretical maximum on a standard unweighted scale. There were thousands of them. Some showed GPAs of 4.5, others 5.2, a handful as high as 6.0.

"Weighted GPAs?" Torres suggested. Some districts used weighted scales that awarded extra points for honors and AP courses.

"Lakeview doesn't," Whitfield said. "Never has. The SIS is configured for a 0-to-4 scale. These are entry errors — the migration script didn't validate upper bounds on float fields. Anything a clerk typed in got carried over."

The GPAs were the beginning. Over the next week, the team catalogued a growing list of anomalies. Class sizes of 60, 80, even 150 — numbers that suggested either a stadium lecture hall or a data-entry clerk who confused class size with total grade-level enrollment. Discipline incident counts suggesting that some students had been written up a dozen times in a single semester, which was possible but warranted scrutiny. And an attendance rate field that, for a small number of students, showed perfect 0.99 attendance while their discipline records and study hours told a very different story.

"The entry errors are concentrated," Anand observed, projecting a missingness heat map onto the conference room screen. "About five percent of records — roughly fifteen thousand — have at least one field with a value that's technically numeric but operationally meaningless. Class size and discipline incidents are the worst offenders, but GPA is close behind."

Beyond the entry errors, approximately three percent of records — nine thousand — were missing values entirely. The gaps appeared in six columns: family income, SAT score, study hours per week, attendance rate, sleep hours, and stress level. The missingness was not random. Family income was disproportionately absent for students at public schools. SAT scores were missing for younger students who hadn't yet taken the exam. Sleep hours and stress level — both self-reported — were absent in clusters that Anand suspected mapped to specific schools where the well-being survey had been administered inconsistently.

And then there were the outliers. Six hundred records — a fraction of a percent — contained values so extreme that they defied plausibility. SAT scores in the 50-to-400 range, below the theoretical minimum of 400 on the modern scale. Family incomes exceeding $800,000, with a handful above $2 million, in a district where the median household income was under $60,000. Weekly study hours of 80, 100, 120 — numbers that would leave no time for sleeping, eating, or attending the classes the student was ostensibly studying for.

"So the dataset is a mess," Carmen said.

"The dataset is a *realistic* mess," Torres corrected. "This is what every SIS migration looks like. The question isn't whether the data has problems. The question is whether the problems are manageable — and whether they're biased."

He was right, and Carmen knew it. If the missing family income records were concentrated among low-income families — the very population the early-warning system was supposed to protect — then any model trained on the complete cases would be learning from a biased sample. The errors and omissions weren't just noise. They were a mirror of the district's institutional blind spots.

---

## III. The Model That Worked Too Well

Six weeks into the project, Torres presented the team's first classification model. The target was `academic_performance` — a three-level variable (High, Medium, Low) that the district used for internal tracking. The model would serve as the early-warning system's front end: flag students in the Low category for intervention, monitor students in the Medium category for signs of decline, and leave the High performers alone.

The results were strong. The model distinguished the three performance tiers with reasonable accuracy across multiple algorithms. Feature importance analysis told a coherent story: GPA, attendance rate, study hours, and SAT scores were the top academic predictors. Extracurricular involvement and sleep hours contributed modestly. Stress level was a surprisingly weak signal on its own but interacted with other variables in ways the team was still unpacking.

The trouble started when Torres scrolled to the bottom of the feature importance chart.

"Family income," he said, pointing to a bar that ranked among the top five most important features. "And parent education level. They're both highly predictive. Family income is the single strongest non-academic predictor in the model."

The room went quiet.

Carmen had expected this. The education research literature was unambiguous: socioeconomic status was one of the strongest predictors of academic outcomes in virtually every large-scale study ever conducted. But knowing it intellectually and seeing it in her own district's data were different experiences.

"Run it without them," she said.

Torres had already anticipated the request. "I did. The model's classification accuracy drops measurably. More importantly, the model's ability to identify students in the Low performance category — the students we most need to flag — degrades. Without socioeconomic features, we miss more of the students who are struggling."

Anand pulled up the regression model — the second deliverable of the initiative. The target here was `college_readiness_score`, a continuous index on a 10-to-100 scale that the district used to estimate a student's preparedness for postsecondary education. The mean score across the district was in the low 40s, but the distribution had a long right tail: a minority of students scored above 70, while the bulk of the population clustered between 20 and 50.

The regression results were even more troubling. Family income and parent education were among the most powerful predictors. The model was essentially saying: tell me how much money a student's family makes and whether their parents went to college, and I can give you a reasonable estimate of their college readiness score — before I know anything about their GPA, their study habits, or their teachers.

"It works," Torres said. "Technically, it works very well. But what it's telling us is that college readiness in this district is largely a function of socioeconomic advantage. The model doesn't predict who's *ready*. It predicts who's *privileged*."

---

## IV. The Equity Director's Objection

Carmen had scheduled a progress review with the superintendent's office for the following week. She had not expected Diane Marchetti to be in the room.

Marchetti was Lakeview's Director of Equity and Inclusion, a former civil rights attorney who had spent a decade in education policy before joining the district. She had a reputation for asking uncomfortable questions and an institutional memory that stretched back further than most of the administrators she now challenged.

Carmen walked the room through the team's findings: the data quality issues, the classification model, the regression results, the dominance of socioeconomic features. She had prepared carefully, anticipating technical questions about model validation and performance metrics.

Marchetti's question was not technical.

"If a teacher opens this early-warning dashboard and sees a student flagged as 'high risk,'" Marchetti said, "and the reason that student is flagged is because their family income is below $30,000 and their parents didn't go to college — what happens next?"

Carmen began to answer, but Marchetti continued.

"I'll tell you what happens. The teacher lowers their expectations. Not consciously. Not maliciously. But the research is clear — and I know Dr. Torres has read Rosenthal and Jacobson. Teacher expectations affect student outcomes. If you tell a teacher that a student is likely to fail, you increase the probability that the student *will* fail. Your early-warning system isn't predicting the future. It's *creating* it."

Torres shifted in his chair. He had, in fact, read Rosenthal and Jacobson — the famous "Pygmalion in the Classroom" study demonstrating that teacher expectations, even when based on fabricated test scores, measurably influenced student achievement. The effect had been replicated dozens of times across different contexts and decades.

"The alternative," Torres said carefully, "is that we don't flag those students at all. And they continue to fall through the cracks the way they've been falling through for years. The eight-point enrollment drop didn't happen because we were paying too much attention to disadvantaged students."

"I'm not saying ignore them," Marchetti replied. "I'm saying the mechanism matters. There's a difference between an early-warning system that says 'this student needs more support because their attendance is declining and their grades are slipping' and one that says 'this student needs more support because they're poor.' The first gives a teacher something actionable. The second gives them a bias."

Superintendent Okonkwo, who had been listening in silence, leaned forward. "Carmen, is there a version of this model that works without family income and parent education?"

"There is," Carmen said. "It's less accurate. Specifically, it's worse at identifying the students in the Low performance category — the students the initiative is designed to help."

"And if you remove those variables," Marchetti pressed, "does the model just find proxies? School type, zip code, AP course access — things that correlate with income?"

Carmen glanced at Torres, who nodded slowly.

"Probably," Carmen admitted. "The socioeconomic signal is embedded in the data in ways that can't be fully removed by dropping two columns. The question isn't whether the model uses income. The question is whether it uses it explicitly — where we can see it, audit it, and control for it — or implicitly, through proxies we can't easily monitor."

The room was silent for a long moment.

"I need a recommendation," Okonkwo said. "Not an analysis — a recommendation. The board presentation is in six weeks, and the Equity Council reviews everything before it goes to the board. Whatever we build, it has to survive both rooms."

---

## V. Two Rooms, One System

Carmen spent the next three weeks rebuilding the models with her team, running scenario analyses, and preparing for two very different audiences.

The first was the District Equity Council — a panel of community members, parents, teachers, and advocacy representatives that reviewed all major district initiatives for fairness and potential disparate impact. The Council had the authority to delay or block any program that it determined would disproportionately harm historically underserved student populations. Marchetti sat on the Council.

The second was the School Board itself — seven elected members who controlled the district's budget and had already approved the $2.4 million for the College Readiness Initiative. They wanted results. The eight-point enrollment drop was a political liability, and several board members faced re-election in the fall. They wanted a system that worked, and they wanted it operational before the next academic year.

The tension between the two audiences was the tension at the heart of the project. The Equity Council would scrutinize the model for bias and potential harm. The Board would scrutinize it for accuracy and return on investment. Carmen needed a system that could satisfy both — or she needed to make a compelling case for why satisfying both simultaneously was impossible, and which tradeoff the district should accept.

Her team had identified three possible approaches:

The first was the full model — all features included, socioeconomic variables front and center. It was the most accurate, particularly for identifying at-risk students. But it was the most vulnerable to the self-fulfilling prophecy critique, and Marchetti would challenge it.

The second was the redacted model — socioeconomic features removed entirely. It was less accurate, particularly in the tails where it mattered most. And as Carmen had acknowledged, the model likely captured the socioeconomic signal through proxies anyway, making the redaction cosmetically clean but analytically dishonest.

The third was something Torres had been developing quietly: a tiered system that used socioeconomic data for *resource allocation* at the school and program level — where to place tutoring centers, which schools needed more counselors, how to distribute AP course access — but excluded it from the individual student-level early-warning flags. The student-facing model would use only behavioral and academic signals: attendance trends, grade trajectories, study engagement, sleep patterns. The system-level model would use everything, including income and parent education, to ensure that resources flowed to the communities that needed them most.

It was elegant. It was also untested.

Carmen opened her laptop and began drafting the presentation. Three hundred thousand records. Twenty-two columns. An eight-point enrollment drop and a $2.4 million mandate. A model that worked and an objection she couldn't dismiss. Two rooms to convince, and a question that the data alone could not answer: When does identifying a struggling student become labeling them?

She thought of the students behind the rows — the ones whose family income cells were empty, whose GPAs had been mangled by a migration script, whose stress levels might be a 9 but whose records said nothing at all. The early-warning system was supposed to see them before they fell. But if seeing them meant defining them by their disadvantage, was the system helping — or was it simply formalizing what the hallways already whispered?

The cursor blinked on an empty slide. She started typing.

---

## Your Assignment

You are a member of Dr. Reyes's analytics team at Lakeview Unified School District. Using the district's 300,000-record student database, you will work through four phases — mirroring the real-world arc of an education analytics engagement: from data audit to board room presentation.

For structured analytical exercises that complement this case, see the companion task set in `documentation/suggested_tasks/education_tasks.md`.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

Lakeview's dataset is large and feature-rich — but it carries the scars of a Student Information System migration, forty-seven schools with different documentation practices, and a student population spanning the full socioeconomic spectrum. Your first task is to determine what you can trust, what you can't, and what you must handle with care.

**Guiding questions:**
- You have 300,000 records with 22 columns. Approximately 9,000 records have missing values and 15,000 have suspected entry errors. Before examining specific columns, what framework would you use to distinguish between data that is missing completely at random (MCAR), missing at random (MAR), and missing not at random (MNAR)? Why does this distinction matter when the model's purpose is to identify disadvantaged students?
- Whitfield's team found GPAs above 4.0, class sizes exceeding 100, and discipline incident counts that strain credulity. Design a data quality audit strategy that goes beyond null checks and range validation. What domain knowledge about school operations would you bring to bear?
- The SIS migration occurred the previous summer. How would you use the `enrollment_date` field to investigate whether data quality varies by time period? What visualization would you create, and what pattern would confirm a migration artifact?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, implausible entries, distributional anomalies, and potential artifacts of the SIS migration. Investigate whether the missingness is random or structured: does it correlate with school type, student demographics, or enrollment timing? This report must convince both Dr. Reyes's team and the School Board that the data foundation is understood — warts and all.

---

### Phase 2: The Prediction Challenge

Lakeview must build two predictive systems for the College Readiness Initiative — one for early warning, one for college preparation.

#### Part A — Academic Performance Classification

The district needs an early-warning system to flag students at risk of low academic performance. Predict `academic_performance` (High / Medium / Low).

**Guiding questions:**
- The target has three classes. What challenges does this create for model training and evaluation? Propose at least two strategies for addressing any class imbalance.
- In an early-warning system, what is the cost of classifying a Low-performing student as High versus classifying a High-performing student as Low? How would you encode this asymmetry into your evaluation framework? What metric(s) would you prioritize over simple accuracy?
- Which features are most predictive? Do the drivers of academic performance differ across school types (Public, Charter, Private)? Are there features that are surprisingly uninformative — or surprisingly powerful?

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with educationally appropriate metrics, and interpretation. Address the asymmetry of misclassification — missing a struggling student is not the same as over-flagging a thriving one. Conclude with a recommendation: how should Lakeview's school counselors use this model at the start of each semester?

#### Part B — College Readiness Regression

The district needs to predict which students are prepared for postsecondary success. Predict `college_readiness_score`.

**Guiding questions:**
- Examine the distribution of college readiness scores across the district. What does the distributional shape tell you about the student population? How would this affect your choice of regression model and error metric?
- Which factors are most strongly associated with college readiness? Are these factors modifiable (e.g., study habits, tutoring, AP courses) or fixed (e.g., family income, parent education)? What are the implications for intervention design?
- The superintendent wants to identify students who are "on the bubble" — close to college-ready but not there yet. How would you use your regression model for this purpose? What threshold would you set, and how would you communicate the uncertainty to school administrators?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis, preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Distinguish between modifiable and non-modifiable factors. Conclude with a recommendation to Dr. Reyes: which students should receive priority access to tutoring, AP courses, and college counseling — and what does the data say about the expected impact?

---

### Phase 3: The Ethical Crossroads

Torres's analysis revealed that family income and parent education are among the most powerful predictors of both academic performance and college readiness. Including them improves the model's ability to identify at-risk students. Marchetti sees a line being crossed.

**Guiding questions:**
- Should Lakeview include family income and parent education as features in the student-facing early-warning model? Defend your position with both analytical and ethical reasoning. Consider: what happens if socioeconomic variables are excluded but the model captures their effect through correlated features like school type, AP course access, and extracurricular involvement?
- Marchetti argues that a model driven by socioeconomic status is "early labeling, not early warning." Torres argues that excluding the strongest predictors is "willful blindness." Is there a middle path — a way to use socioeconomic information to *allocate resources equitably* without *labeling individual students* by their family's circumstances? What would that system look like in practice?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on whether and how socioeconomic data should be used in Lakeview's early-warning system. Defend your position with both analytical evidence from the data and ethical reasoning grounded in the education literature. Address the self-fulfilling prophecy concern directly — cite the mechanism by which teacher expectations affect student outcomes, and explain how your proposed system mitigates or accepts that risk. If you propose a tiered approach like Torres's, specify exactly how it would work in practice.

---

### Phase 4: The Board Room

It is presentation day. Carmen stands before two audiences: the District Equity Council and the School Board. The $2.4 million initiative — and the district's credibility — depends on this presentation.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes a superintendent, an equity director, a school board chair, a parent advocacy representative, and a data-skeptical principal who has been teaching for thirty years. Communicate: (a) the early-warning system's capabilities and validation results, (b) how it integrates into school counselors' existing workflows across diverse school types, (c) how Lakeview will monitor for bias and the self-fulfilling prophecy effect, and (d) what the data reveals about the eight-point college enrollment drop — is it a failure of students, or a failure of systems? No jargon. No hedging. Both rooms need to trust the system and the people behind it.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in Lakeview's data that is not covered by Phases 1–3? A pattern across school types that challenges assumptions about charter effectiveness, an unexpected relationship between sleep and college readiness that dwarfs the tutoring effect, a subpopulation that the models consistently misjudge, or a finding that reframes the "college readiness crisis" as something the district has been measuring wrong all along. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

| Resource | Path |
|----------|------|
| Dataset | `datasets/education/synthetic_education_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/education_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/education_tasks.md` |

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Label Maker." *From Data to Decisions*, Case 9. University of North Texas.
