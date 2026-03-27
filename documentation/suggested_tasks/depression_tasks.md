# Depression Dataset — Analytical Questions

Use the Depression dataset (`synthetic_depression_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a mental-health programme analytics team would face. Your task is to determine the best analytical approach, identify relevant features, build and evaluate models, and communicate actionable insights.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Before any modeling, conduct a thorough data quality assessment. What issues do you find (missing values, impossible PHQ-9 scores, extreme entries)? How would you handle missing clinical scores differently from missing lifestyle data? Propose and justify a cleaning pipeline.

**Q2. Patient Population Profiling**
The programme director wants to understand "who is seeking help." Using EDA and visualization, describe the patient population across demographics, clinical history, lifestyle, and social factors. Are there natural groupings? How do screening scores (PHQ-9, GAD-7) relate to lifestyle and social variables?

---

## 📊 Classification Challenges

**Q3. Depression Severity Prediction**
Build a classification model to predict `depression_severity` (None/Mild, Moderate, Severe). Which clinical and behavioural features are the strongest predictors? How could a screening clinic use this model to triage patients for different levels of care?

**Q4. Model Comparison**
Compare at least three different classification algorithms for severity prediction. In a mental-health setting, what are the consequences of misclassification — is it worse to miss a Severe case or to over-refer a Mild case? How does this inform your model choice?

**Q5. Subgroup Analysis**
Investigate whether depression risk factors differ across genders, age groups, or employment statuses. Do certain subgroups have different warning signs? Should the screening programme use different criteria for different populations?

---

## 📈 Regression Challenges

**Q6. Recovery Score Prediction**
The treatment team wants to predict `recovery_score` early in treatment to set realistic goals. Build a regression model, report its accuracy (RMSE, MAE, R²), and identify the factors most strongly associated with better recovery outcomes. What modifiable factors should clinicians focus on?

**Q7. Feature Engineering**
Can you improve your recovery model by creating new features? Consider composite measures (social support × therapy engagement), ratio features (sleep quality / stress indicators), or protective-factor scores. Report the before/after model performance.

---

## 🧩 Unsupervised Learning

**Q8. Patient Segmentation**
Use clustering techniques to identify distinct patient profiles. How many meaningful segments exist? Describe each in clinical terms — what treatment approach would you recommend for each group?

**Q9. Risk Factor Patterns**
Using the clusters from Q8 or an alternative approach, investigate whether certain risk factors tend to co-occur. For example, do patients with high isolation also tend to have substance use and poor sleep? What does this "clustering of vulnerabilities" imply for treatment design?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using model-agnostic interpretability tools (e.g., SHAP, permutation importance), analyze which features matter most for both depression severity and recovery score. Are the drivers of severity the same as the drivers of recovery, or do they differ? What does this tell us about the difference between "getting depressed" and "getting better"?

**Q11. Actionable Recommendations**
Based on all your analyses, prepare a one-page executive summary for the programme director. Include: (a) three critical findings about depression risk and recovery, (b) two specific programme recommendations (screening improvements, treatment modifications, or resource allocation), and (c) a plan for improving patient data collection.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
