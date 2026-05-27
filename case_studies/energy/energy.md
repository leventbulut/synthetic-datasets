# The Retrofit Equation

**A Data Science Case Study in Building Energy Efficiency and Environmental Justice**

**From Data to Decisions** | A $50M Fund, 350,000 Buildings, and the Question of Who Gets Helped First — Energy Analytics

---

> **Data Resources**
>
> - Dataset: `datasets/energy/synthetic_energy_20250901.csv`
> - Data Dictionary: `documentation/data_dictionaries/energy_dictionary.md`
> - Suggested Tasks: `documentation/suggested_tasks/energy_tasks.md`
> - Exhibit A: Clean Buildings Act Legislative Summary — `case_studies/energy/exhibits/exhibit_A.md`
> - Exhibit B: GreenGrid Utilities Building Portfolio Dashboard — `case_studies/energy/exhibits/exhibit_B.md`

---

## I. The Mandate

Dr. Amara Osei arrived at her office on a Monday morning in early March to find four messages waiting. The first was from her chief of staff, flagging a calendar collision — the Public Utilities Commission hearing had been moved up by two weeks. The second was from GreenGrid Utilities' general counsel, attaching a red-lined copy of the regulatory compliance framework. The third was from the State Energy Office, requesting a preliminary building inventory by end of month.

The fourth was from the Governor's press secretary, with a single attachment: the signed text of the Clean Buildings Act.

The legislation had been expected. The vote had not been close. But the specifics, now locked into statute, were more aggressive than anyone in GreenGrid's executive suite had anticipated (see Exhibit A). A mandatory 30% reduction in building energy consumption across the utility's service territory within five years. A $50 million Retrofit Investment Fund administered through participating utilities, with GreenGrid responsible for roughly $50 million allocated to its territory. And accountability provisions that gave the Public Utilities Commission authority to levy penalties against utilities that failed to demonstrate measurable annual progress.

"Fifty million dollars sounds like a lot of money," said James Kaplan, GreenGrid's Chief Operating Officer, during the emergency leadership call that afternoon. "Until you divide it by 350,000 buildings."

That arithmetic — roughly $143 per building if distributed equally — was the problem in miniature. The fund was large enough to matter but nowhere near large enough to subsidize every building in GreenGrid's service territory. The legislation required utilities to identify and prioritize the buildings where retrofit investments would yield the greatest energy savings. Every dollar spent on a building that didn't need it was a dollar diverted from one that did.

Amara, who held a doctorate in environmental engineering and had spent seven years building GreenGrid's sustainability analytics capability, was the obvious choice to lead the effort. The COO made it official before the call ended: Amara would develop the targeting model that determined which buildings received retrofit subsidies, in what order, and at what funding level.

"You'll need data," Kaplan said. "Good data."

"I'll need data," Amara agreed. "I'm less certain about the 'good' part."

---

## II. Three Systems, One Spreadsheet

GreenGrid Utilities served a metropolitan region of approximately 350,000 buildings spanning four sectors: residential, commercial, industrial, and institutional. The utility's Building Management System — a term that dignified what was, in practice, a database assembled from three incompatible sources — contained one record per building, each with 21 data fields covering building profiles, systems and equipment characteristics, weather conditions at the time of the most recent energy reading, and energy consumption metrics.

The three source systems had never been designed to talk to each other. Utility billing records captured energy consumption and meter data with reasonable fidelity — bills, after all, had to be accurate enough to collect revenue. Municipal building permits recorded structural characteristics: floor area, building age, building type. But these records reflected the building as it existed at the time of permitting, not necessarily its current state. A building permitted as a 500-square-meter warehouse that had since been subdivided into six residential units still appeared in the permit database as a warehouse.

The third source was the worst. Self-reported energy audits, submitted by building owners as part of a previous voluntary efficiency program, captured equipment data — HVAC system age, insulation ratings, window efficiency, solar panel installations, appliance counts. These audits were voluntary, unverified, and filled out by building owners who had every incentive to overstate their building's condition and every opportunity to misremember when the furnace was last replaced.

"The billing data is the most reliable, the permit data is the most outdated, and the audit data is the most creative," said Nolan Reeves, a senior data engineer on Amara's team, after his first week profiling the extract. "Together, they give us 350,000 records across 21 columns. Individually, they give us three different stories about the same buildings."

The numbers told a sprawling story. Building ages ranged from 1 to 80 years, with a center around 16 years — a portfolio skewed toward newer construction but with a long tail of aging structures. Floor areas spanned from 50 square meters for small residential units to 20,000 square meters for large industrial facilities, with a center near 665 square meters. Occupant counts followed a Poisson-like distribution centered around 12, ranging from single-occupant residences to buildings housing 200 or more people. Energy consumption itself was log-normally distributed, clipped between 50 and 50,000 kWh, with the bulk of readings clustering in a band but a long right tail of energy-intensive buildings driving the aggregate numbers.

Equipment data was similarly varied. Insulation ratings ranged from 15 to 100 on a composite quality scale, centered around 50. HVAC system ages ranged from six months to 25 years, with a center around 6 years. Window thermal efficiency ratios ran from 0.20 to 0.95, centered near 0.50. Solar panel capacity was zero for roughly 40% of buildings — no panels installed — while the remainder ranged up to 200 kW, with a center near 4.5 kW for buildings that had them. Peak demand ranged from 2 kW to 500 kW, centered around 20 kW.

Weather conditions at the time of the most recent reading added another layer: outdoor temperatures spanning from −20°C to 45°C (centered near 15°C), humidity from 10% to 95% (centered near 50%), and daylight hours varying with season.

"That's a lot of variation," Amara observed, scanning Nolan's summary tables. "How much of it is real, and how much is noise?"

Nolan set down the printout. "That's what I need to tell you about."

---

## III. The Scars in the Data

The data quality problems announced themselves quickly, once Nolan's team knew where to look.

The first layer was missing values. Approximately 10,500 records — roughly 3% of the dataset — had gaps in fields that mattered most for efficiency modeling: insulation ratings, window efficiency, outdoor temperature, peak demand, and HVAC age. The missingness was not random. It clustered in patterns that Nolan suspected were tied to which source system had contributed the record and when the building had last been audited.

"The fields we need most for predicting efficiency are the ones building owners were least reliable about reporting," he told Amara. "If we drop every record with a missing value, we lose ten thousand buildings. If we impute carelessly, we're inventing insulation ratings for buildings we've never inspected."

The second layer was outliers — rare but spectacular. About 700 records, a fraction of a percent, contained values that stopped the eye: floor areas of 40,000 to 100,000 square meters — buildings the size of a football stadium in a service territory that contained no football stadiums. Peak demands of 1,000 to 5,000 kW from buildings that, based on their other characteristics, should have drawn a fraction of that. Occupant counts of 500 to 2,000 in buildings with floor areas that would give each person less space than a phone booth.

"Are these real?" Amara asked.

"Some could be data entry errors — someone typed an extra zero," Nolan said. "Some could be aggregation artifacts — a campus of buildings rolled up into a single record. And some might be genuine. A large industrial complex could legitimately have a floor area of 40,000 square meters. But at 100,000? That's a data problem, not a building."

The third and most pervasive layer was entry errors — roughly 17,500 records, about 5% of the dataset, where the values were not missing or extreme but simply wrong in ways that required domain knowledge to recognize. Building ages of 100 to 300 years in a metropolitan area where the oldest structures dated to the late nineteenth century. HVAC system ages of 40 to 100 years for equipment with a typical service life of 15 to 25 years. Appliance counts of 80 to 200 per building — numbers that would imply a residential kitchen equipped like a commercial restaurant.

"These came from the self-reported audits," Nolan said. "A building owner writes '150' in the appliance count field, and nobody catches it because there's no validation on the form. Another one reports an HVAC age of 60 years — maybe they're reporting the age of the building, not the system."

Amara studied the summary. "So we have three layers: missing values that aren't random, outliers that might be errors or might be real, and entry mistakes that are definitely wrong but buried in the middle of the distribution where they're hard to catch."

"Welcome to building management data," Nolan said.

---

## IV. Two Targets, Two Problems

Despite the data quality challenges, the Clean Buildings Act's timeline was not negotiable. Amara structured the analytical work into two parallel tracks, each addressing a different question the State Energy Office would ask at the hearing.

**Track One: Efficiency Classification.** The dataset included an efficiency level classification for each building — High (0), Medium (1), or Low (2) — derived from a composite efficiency score that accounted for building characteristics, equipment quality, and energy usage relative to building size and type. The distribution across three classes provided the basis for the most operationally urgent question: which buildings were currently performing poorly and would benefit most from retrofit investment?

"The state wants us to target the Low-efficiency buildings first," said Keiko Tanaka, GreenGrid's Director of Regulatory Affairs. "That's the political logic. Spend the retrofit money where the waste is greatest."

"The political logic and the analytical logic may not agree," Amara replied. "We need to understand what drives a building into the Low-efficiency tier — and whether the features that predict efficiency are the same features we can actually change through retrofits."

The classification challenge was compounded by what the model would need to do in practice. GreenGrid didn't just need to predict which buildings were currently inefficient — it needed to predict which buildings would respond to intervention. A building classified as Low-efficiency because of its age and building type was a fundamentally different retrofit candidate than one classified as Low-efficiency because of a failing HVAC system. The first required a philosophical conversation about building replacement; the second required a new furnace.

**Track Two: Energy Consumption Prediction.** The State Energy Office needed demand forecasts — building-level predictions of energy consumption for planning purposes and, critically, for estimating retrofit savings. If GreenGrid could accurately predict how much energy a building consumed under current conditions, it could estimate how much energy that building *would* consume after a retrofit, and therefore quantify the expected savings per dollar invested.

The consumption data was log-normally distributed, centered near a modest value but with a long right tail stretching toward 50,000 kWh. Understanding what drove buildings into that upper tail — whether it was building size, equipment age, weather exposure, occupant count, or some interaction of these factors — was as important as the point predictions themselves.

"Two models," Amara told her team. "One tells us which buildings need help. The other tells us how much help they need. Together, they give us a defensible allocation strategy for $50 million."

---

## V. The Equity Problem

It was during the fourth week of model development that Nolan brought Amara a finding that complicated everything.

"I've been profiling efficiency levels across every dimension in the dataset," he said, pulling up a set of cross-tabulations on his monitor. "Building age, insulation rating, HVAC age, solar capacity — they all matter. But look at this." He pointed to the breakdown by building type.

The pattern was difficult to ignore. Industrial and institutional buildings were systematically associated with lower efficiency classifications. They consumed more energy in absolute terms, had older and less efficient equipment on average, and showed lower insulation ratings. From a purely analytical standpoint, `building_type` was among the most informative features in the classification model — and it pointed unmistakably toward targeting industrial and institutional buildings first.

The arithmetic was seductive. A single industrial facility retrofit could save as much energy as retrofitting dozens of residential buildings. With a fixed $50 million fund and a statutory mandate to achieve a 30% reduction, the highest-impact strategy was to concentrate spending on the buildings where each dollar saved the most kilowatt-hours.

"If we optimize purely for energy reduction per dollar," Nolan said, "we fund industrial and institutional retrofits first. The residential sector — especially small, older residential buildings — falls to the back of the queue."

Amara knew what was coming next, because the Environmental Justice Coalition had already sent a letter.

The coalition, representing community organizations across GreenGrid's service territory, argued that small residential buildings — particularly those in older, lower-income neighborhoods — were individually less wasteful than industrial facilities but collectively represented the most vulnerable population. Their residents spent a higher proportion of household income on energy bills. They lived in buildings with the oldest equipment, the worst insulation, and the fewest resources to fund improvements on their own. An efficiency program that bypassed them in favor of industrial facilities would deepen the energy burden on the people least able to bear it.

"They're not wrong," Amara said, reading the letter. "A low-income family paying 12% of their income on energy bills gets nothing from a model that optimizes aggregate kilowatt-hour savings. The model doesn't see their bills. It sees their building's total consumption — which is small."

"But the state mandate isn't about energy bills," Nolan countered. "It's about total consumption reduction. If we spread the fund across thousands of small residential buildings, we might not hit the 30% target. And if we miss the target, the PUC penalizes GreenGrid — which raises rates for everyone, including those same low-income families."

The dilemma had no clean resolution. Optimizing for maximum energy savings per dollar would satisfy the regulatory mandate but concentrate benefits among building owners who were least likely to need public subsidy. Optimizing for equity would direct funds toward the most vulnerable populations but might not achieve the statutory reduction target, triggering penalties that would ultimately be passed on to ratepayers.

"So we can be efficient and inequitable," Amara said, "or we can be equitable and risk missing the mandate."

"Or," Nolan said, "we can try to find a middle path. But any middle path involves trade-offs that the Public Utilities Commission needs to understand and approve. This isn't a modeling decision. It's a policy decision."

---

## VI. Preparing for the Hearing

By the end of the second month, Amara had enough preliminary work to structure the presentation for the Public Utilities Commission and the State Energy Office. She outlined the agenda with the COO and GreenGrid's Director of Regulatory Affairs.

The presentation would need to cover three areas.

First, **data quality and trustworthiness.** Before any model results, the commission needed to understand the limitations of the building management data. The 10,500 records with missing values, the 17,500 entry errors, the 700 outliers — these were not footnotes. They were foundational constraints on what any targeting model could reliably predict. Amara wanted the commission to understand that a retrofit allocation model built on self-reported energy audits and outdated permit data would produce imperfect targeting, regardless of the sophistication of the algorithm.

Second, **predictive models and their limitations.** The efficiency classifier and the consumption regression model would be presented side by side, with transparent assessments of performance. Amara planned to show the commission where the models worked well, where they struggled, and — critically — the relationship between building type and efficiency classification. The commission needed to understand that the model's most statistically powerful finding was also its most politically sensitive.

Third, **the equity question.** This was the discussion Amara dreaded most. The commission included members appointed by the Governor with strong commitments to environmental justice and members with equally strong commitments to fiscal accountability. Presenting a model that targeted industrial buildings first without addressing the equity implications would be irresponsible. Presenting a model that prioritized residential buildings without acknowledging the risk to the 30% mandate would be dishonest.

"The Clean Buildings Act is the burning platform," Keiko Tanaka said during the prep meeting. "But the commission will also ask: does this allocation model leave behind the communities that need help the most?"

Amara didn't have a clean answer. She suspected the commission wouldn't either — and that was precisely the conversation that needed to happen.

---

## Your Assignment

You have been retained as an external analytics consultant supporting Dr. Amara Osei's initiative. Using GreenGrid Utilities' 350,000-building energy dataset, you will work through four phases — mirroring the real-world arc of a building energy analytics engagement: from data audit to public hearing.

---

### Phase 1: Discovery & Diagnosis

Before any model can be trusted, the data must be understood.

GreenGrid's Building Management System was assembled from three incompatible sources — utility billing records, municipal building permits, and self-reported energy audits — each with different capture practices, validation standards, and incentive structures. Your first task is to determine how deep those scars go.

**Guiding questions:**
- Where are the data quality issues concentrated — in specific building types, equipment fields, or source system patterns? Do the missingness patterns align with the self-reported audit narrative, and which fields are most affected?
- How would you distinguish the ~700 genuine outliers from the ~17,500 entry errors? What domain knowledge would you apply to separate a legitimate 40,000 m² industrial complex from a data entry error, and what are the downstream consequences of each cleaning strategy?

**Deliverable:** A **Data Quality Report** (1–2 pages with supporting code or visualizations). Document every issue you discover — missing values, implausible metrics, entry errors, and distributional anomalies. For each issue, state what you found, quantify its scope, and recommend a handling strategy. This report should answer Amara's foundational question: *Is this data trustworthy enough to build a retrofit targeting model on?*

---

### Phase 2: The Prediction Challenge

The Clean Buildings Act mandates measurable progress. Two models. Five years.

#### Part A — Efficiency Classification

The State Energy Office wants to know which buildings to target first. Predict `efficiency_level` (3-class: High / Medium / Low).

**Guiding questions:**
- What building characteristics are most predictive of efficiency level? Which are modifiable through retrofits (insulation, HVAC, windows) and which are structural constraints (building age, floor area, building type)? How does this distinction affect the practical utility of the classifier for retrofit targeting?
- Efficiency classification is a three-class problem. What is the distribution across classes, and what metric should you optimize? Consider the operational asymmetry: classifying a Low-efficiency building as High means it never receives a retrofit subsidy. Classifying a High-efficiency building as Low wastes scarce fund dollars.

**Deliverable:** A **Classification Notebook** (.ipynb — fully executable, clearly commented). Must include: EDA, your cleaning pipeline (informed by Phase 1), feature engineering, at least two distinct algorithms, evaluation with operationally appropriate metrics, and interpretation. Address the misclassification cost asymmetry explicitly. Conclude with a clear recommendation: which building attributes should GreenGrid prioritize in its retrofit targeting, and how would you embed this model into the subsidy allocation workflow?

#### Part B — Energy Consumption Regression

The State Energy Office needs demand forecasts and retrofit savings estimates. Predict `energy_consumption_kwh`.

**Guiding questions:**
- Energy consumption is log-normally distributed with a long right tail. What drives buildings into that upper tail? Which combinations of building type, floor area, equipment age, and weather conditions produce the highest consumption?
- How should GreenGrid use consumption predictions for retrofit savings estimation? If the model predicts a building's current consumption, and the retrofit changes specific features (e.g., HVAC age, insulation rating), can you estimate post-retrofit consumption and therefore the expected savings? Where should the State Energy Office trust these estimates, and where should it be skeptical?

**Deliverable:** A **Regression Notebook** (.ipynb — fully executable, clearly commented). Must include: target variable analysis (investigate the log-normal distribution and right tail), preprocessing, feature engineering, at least two regression approaches, residual analysis, and interpretation. Conclude with a recommendation to the State Energy Office: how should consumption predictions inform the allocation of the $50 million Retrofit Investment Fund? Characterize the error distribution — where does the model perform well, and where does it struggle?

---

### Phase 3: The Ethical Crossroads

Nolan's analysis revealed that building type is a powerful predictor of efficiency level. Targeting industrial and institutional buildings first maximizes kilowatt-hour savings per dollar. But it directs the retrofit fund away from low-income residential buildings whose occupants bear the highest energy burden relative to income.

**Guiding questions:**
- Should the retrofit targeting model optimize for maximum aggregate energy savings (favoring industrial/institutional buildings) or for equitable distribution of benefits (favoring residential buildings in underserved communities)? Construct arguments for both positions. Is there a hybrid approach that achieves meaningful progress on both objectives — and what does it sacrifice?
- If GreenGrid deploys an allocation model that systematically deprioritizes residential buildings, what are the consequences for environmental justice, public trust, and the long-term political viability of efficiency mandates? Could an efficiency-first approach undermine the very coalition that passed the Clean Buildings Act?

**Deliverable:** An **Ethics Position Paper** (1 page, single-spaced). Take a clear position on the equity-efficiency trade-off. Defend your position with both analytical evidence from the data and ethical reasoning. Address the counterargument directly. If you propose a hybrid allocation strategy (e.g., tiered funding pools, equity-weighted scoring, building-type-specific targets), specify exactly how it would work and what trade-offs it introduces.

---

### Phase 4: The Board Room

It is two months after the Clean Buildings Act was signed. Dr. Amara Osei stands before the Public Utilities Commission and the State Energy Office. The commission wants a defensible allocation strategy. The state wants measurable progress toward the 30% reduction target. The Environmental Justice Coalition wants assurance that the fund won't bypass the communities that need it most.

**Deliverable A:** An **Executive Brief** (1-page memo OR 5-slide presentation deck). Your audience includes the Public Utilities Commission chair, the State Energy Office director, GreenGrid's COO, and a representative of the Environmental Justice Coalition. Communicate: (a) the scope of GreenGrid's building energy challenge, (b) what your models reveal about which buildings are least efficient and what drives consumption, (c) your recommended allocation strategy for the $50 million Retrofit Investment Fund with implementation roadmap, and (d) the data limitations and model uncertainties the commission should understand. Keiko Tanaka will ask: *"Does this allocation model leave behind the communities that need help the most?"* Be ready.

**Deliverable B:** **The Unsolicited Insight** (free-form, 1 page maximum). The best analysts don't just answer the questions they're given — they find questions nobody thought to ask. What did you discover in GreenGrid's building energy data that is not covered by Phases 1–3? A seasonal pattern that warrants investigation, an unexpected interaction between equipment age and solar capacity, a building type that defies the model's assumptions, or a weather sensitivity profile that suggests operational interventions beyond retrofits. There is no wrong answer — but there is a lazy one. Show us what you see that others might miss.

---

| Resource | Path |
|---|---|
| Dataset | `datasets/energy/synthetic_energy_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/energy_dictionary.md` |
| Suggested Tasks | `documentation/suggested_tasks/energy_tasks.md` |

> The companion task set (`documentation/suggested_tasks/energy_tasks.md`) provides additional analytical questions — including unsupervised learning challenges such as building archetype clustering and weather sensitivity analysis — that complement this case study. Students are encouraged to explore those tasks alongside the four phases above.

---

**From Data to Decisions: An Applied Case Study Series in Data Science**

© 2026 Levent Bulut. All rights reserved.

This case was prepared as a basis for class discussion and is not intended to illustrate either effective or ineffective management of a business situation. All characters, companies, and scenarios are fictional. The accompanying dataset is synthetic and licensed for educational and analytical use.

*Suggested citation:*
Bulut, L. (2026). "The Retrofit Equation." *From Data to Decisions*, Case 11. University of North Texas.
