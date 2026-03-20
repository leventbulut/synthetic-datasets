# Healthcare Dataset — Analytical Questions

Use the Healthcare dataset (`synthetic_healthcare_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a hospital analytics team would face. Your task is to determine the best analytical approach, identify relevant features, build and evaluate models, and communicate actionable insights.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Before any modeling, conduct a thorough data quality assessment. What types of issues do you find (missing values, outliers, implausible entries)? Propose a data-cleaning pipeline and justify your choices — for example, how would you handle missing lab values differently from missing vital signs?

**Q2. Patient Population Profiling**
Hospital leadership wants to understand "who is being admitted." Using exploratory data analysis and visualization, describe the patient population. How do age, diagnosis, department, and insurance type interact? Are there natural groupings that suggest distinct patient profiles?

---

## 📊 Classification Challenges

**Q3. Readmission Risk Prediction**
The Chief Medical Officer needs a model to predict which patients are at high risk of readmission (`readmission_risk`). Build a classification model, evaluate its performance, and present the top factors driving readmission. How should the care coordination team prioritize their post-discharge follow-up?

**Q4. Model Comparison**
Compare at least three different classification algorithms for readmission prediction. Which model performs best, and why? Discuss the trade-off between predictive accuracy and clinical interpretability — which would you recommend to a physician, and why?

**Q5. Class Imbalance & Cost-Sensitive Analysis**
Examine the distribution of readmission risk classes. Is there an imbalance? In a clinical setting, is a false negative (missing a high-risk patient) worse than a false positive? Experiment with cost-sensitive learning or resampling techniques and report how this changes model behavior.

---

## 📈 Regression Challenges

**Q6. Hospital Cost Estimation**
The CFO needs to predict `total_cost` of a patient's stay for budget planning. Build a regression model, report its accuracy (RMSE, MAE, R²), and identify the most important cost drivers. What advice would you give for controlling costs?

**Q7. Feature Engineering**
Can you improve your cost model by creating new features? Consider interactions (e.g., length_of_stay × comorbidity_count), ratios (e.g., medications per comorbidity), or derived clinical indicators. Report before/after model performance.

---

## 🧩 Unsupervised Learning

**Q8. Patient Segmentation**
Use clustering techniques to identify distinct patient segments. How many segments do you recommend? Describe each one in terms that a hospital administrator could understand and act upon.

**Q9. Segment-Specific Modeling**
After identifying patient segments (Q8), build separate readmission models for each segment. Does a segment-specific approach outperform a single global model? What does this tell you about patient heterogeneity?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using model-agnostic interpretability tools (e.g., SHAP, permutation importance), analyze which features matter most for both readmission risk and cost. Are the drivers the same for both targets, or do they differ? Present your findings visually.

**Q11. Actionable Recommendations**
Based on all your analyses, prepare a one-page executive summary for the hospital CEO. Include: (a) the three most critical findings, (b) two specific operational recommendations to reduce readmissions, and (c) a data quality improvement plan for the EHR system.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
