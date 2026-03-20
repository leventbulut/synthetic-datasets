# Telecommunications Dataset — Analytical Questions

Use the Telecommunications dataset (`synthetic_telecom_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a telecom analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find? How would you handle missing network metrics vs. missing billing data? Propose and justify a cleaning strategy.

**Q2. Subscriber Landscape**
The VP of Marketing wants to understand the subscriber base. Using EDA, describe how plan types, usage patterns, service interactions, and billing behavior relate to each other. What subscriber profiles emerge?

---

## 📊 Classification Challenges

**Q3. Churn Prediction**
Build a classification model to predict `churn_prediction` (Retain/At Risk/Likely Churn). Which subscriber behaviors are the strongest early warning signals? How far in advance can you reliably identify at-risk subscribers?

**Q4. Model Comparison**
Compare at least three classification algorithms. Discuss the business value of catching churn early — what is the cost of a false negative (missing a churner) vs. a false positive (wasting a retention offer on a loyal customer)?

**Q5. Contract and Plan Effects**
Investigate whether churn drivers differ between contract types (month-to-month vs. annual) and plan tiers (Basic vs. Premium). Should the retention team use different strategies for each segment?

---

## 📈 Regression Challenges

**Q6. Satisfaction Score Prediction**
The product team wants to predict `satisfaction_score` to identify improvement areas without waiting for surveys. Build a regression model and identify which operational factors have the biggest impact on satisfaction.

**Q7. Feature Engineering**
Can you improve your satisfaction model with new features? Consider usage intensity ratios (data per dollar), service interaction rates, or tenure-adjusted metrics. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Subscriber Segmentation**
Use clustering to discover natural subscriber segments based on usage and behavior. How many segments exist? What tailored offerings would you design for each?

**Q9. Churn vs. Satisfaction Interaction**
Are dissatisfied customers always the ones who churn? Use your segments and models to explore the relationship between satisfaction and churn. Which subscriber profile is "silently churning" (leaving despite appearing satisfied)?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of churn vs. satisfaction. Are they mirror images, or do some factors drive churn without affecting satisfaction (and vice versa)?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the Chief Marketing Officer. Include: (a) three key findings about subscriber retention, (b) two specific retention program recommendations, and (c) a plan for improving service quality monitoring.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
