# Education Dataset — Analytical Questions

Use the Education dataset (`synthetic_education_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a school district analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find (e.g., impossible GPAs, extreme values)? How would you handle missing family income data vs. missing study metrics? Propose and justify a cleaning strategy.

**Q2. Student Population Profiling**
The school board wants to understand "who our students are." Using EDA, describe how academic performance, study habits, family background, and well-being indicators interact. What student profiles emerge?

---

## 📊 Classification Challenges

**Q3. Academic Performance Prediction**
Build a classification model to predict `academic_performance` (High/Medium/Low). Which factors matter most? How could a school counselor use this model for early intervention with struggling students?

**Q4. Model Comparison**
Compare at least three classification approaches. In education, is it more important to correctly identify Low-performing students (recall) or to avoid mislabeling students (precision)? How does this choice affect your model design?

**Q5. Equity Analysis**
Investigate whether the drivers of academic performance differ across school types (Public/Charter/Private) and family backgrounds. Does the model perform equally well for all subgroups, or are there equity concerns that need addressing?

---

## 📈 Regression Challenges

**Q6. College Readiness Prediction**
The district superintendent wants to predict `college_readiness_score` to allocate resources. Build a regression model, identify the most important predictors, and determine whether academic factors or non-academic factors matter more for readiness.

**Q7. Feature Engineering**
Can you improve your readiness model with new features? Consider study efficiency ratios (GPA per study hour), engagement scores (combining extracurriculars + library visits), or stress-adjusted performance. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Student Segmentation**
Use clustering to discover natural student groups. How many groups exist? Describe each in terms that a principal could act upon — what support does each group need?

**Q9. Impact of Interventions**
Students who use tutoring and AP courses may represent a distinct group. Use clustering and conditional analysis to explore whether these interventions are associated with better outcomes, and for which student profiles they matter most.

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of academic performance vs. college readiness. Is a high-performing student always college-ready? What non-academic factors create the gap?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the school board. Include: (a) three key findings about student success drivers, (b) two specific program recommendations (tutoring, AP access, etc.), and (c) a plan for equitable distribution of resources.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
