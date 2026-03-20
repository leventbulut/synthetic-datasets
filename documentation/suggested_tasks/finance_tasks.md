# Finance Dataset — Analytical Questions

Use the Finance dataset (`synthetic_finance_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a bank's risk analytics team would face. Your task is to determine the best analytical approach, identify relevant features, build and evaluate models, and communicate actionable insights.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Before any modeling, conduct a thorough data quality assessment. What types of issues do you find? How would you handle missing financial data differently from demographic data? Propose and justify a cleaning pipeline.

**Q2. Customer Financial Profiling**
The Chief Risk Officer wants a comprehensive picture of the customer base. Using EDA and visualization, describe the relationships between income, credit score, savings behavior, and debt metrics. Are there natural customer archetypes?

---

## 📊 Classification Challenges

**Q3. Credit Risk Prediction**
Build a classification model to predict `credit_risk` (4-class: Very Low to High). Which features are most predictive? How would a loan officer use this model to make faster, more consistent lending decisions?

**Q4. Model Comparison**
Compare at least three different classification algorithms for credit risk. Discuss the trade-off between accuracy, interpretability, and fairness — should the bank be concerned about disparate impact across demographic groups?

**Q5. Multiclass Performance Analysis**
With four credit risk classes, simple accuracy can be misleading. Examine per-class precision, recall, and F1 scores. Which risk level is hardest to predict accurately, and what are the business consequences of misclassification at each level?

---

## 📈 Regression Challenges

**Q6. Fraud Risk Scoring**
Compliance needs a model to estimate `fraud_risk_score` for account prioritization. Build a regression model, evaluate it, and identify the behavioral patterns most associated with elevated fraud risk. How would you set a threshold for flagging accounts?

**Q7. Feature Engineering**
Can you improve your fraud model by engineering new features? Consider ratios (spending-to-income), interaction terms (credit utilization × late payments), or temporal features. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Customer Segmentation for Product Design**
The retail banking team wants to design new financial products. Use clustering to identify distinct customer segments based on financial behavior. How many segments exist, and what product would you design for each?

**Q9. Anomaly Detection**
Instead of supervised fraud scoring, use unsupervised anomaly detection to identify unusual customers. How do the flagged accounts compare to those with high fraud_risk_scores? What are the advantages and limitations of each approach?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, analyze which features drive credit risk vs. fraud risk. Are the drivers the same, or does each target depend on different customer behaviors? Present your findings visually.

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the Chief Risk Officer. Include: (a) the three most important risk drivers, (b) two specific policy recommendations (lending criteria or account monitoring), and (c) a data collection improvement plan.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
