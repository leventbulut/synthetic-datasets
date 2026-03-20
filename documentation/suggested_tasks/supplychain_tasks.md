# Supply Chain Dataset — Analytical Questions

Use the Supply Chain dataset (`synthetic_supplychain_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a procurement and operations analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find? How would you handle missing supplier performance metrics vs. missing logistics data? Propose and justify a cleaning strategy.

**Q2. Supply Chain Landscape**
The VP of Procurement wants a comprehensive overview of the supply chain. Using EDA, describe the relationships between supplier performance, regional patterns, product categories, and logistics complexity. What stands out?

---

## 📊 Classification Challenges

**Q3. Supplier Risk Classification**
Build a classification model to predict `supplier_risk` (4-class: Minimal to Critical). Which supplier attributes are most predictive? How would procurement use this to pre-qualify vendors?

**Q4. Model Comparison**
Compare at least three classification approaches. Consider the cost of misclassification — what happens if a Critical-risk supplier is classified as Minimal? Incorporate this asymmetry into your evaluation.

**Q5. Regional Risk Analysis**
Do supplier risk profiles vary by region? Build a model that accounts for regional differences and analyze whether the company should diversify its supplier base geographically.

---

## 📈 Regression Challenges

**Q6. Total Order Cost Prediction**
Finance needs accurate order cost estimates for budgeting. Build a regression model for `total_cost`, evaluate it, and identify the main cost drivers. Where is the biggest opportunity for cost reduction?

**Q7. Feature Engineering**
Can you improve cost prediction by creating derived features? Consider total order value (quantity × price), efficiency metrics (cost per unit), or supplier composite scores. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Supplier Segmentation**
Use clustering to group suppliers into performance tiers. How many tiers do you recommend? Describe each tier in terms a procurement manager could act upon.

**Q9. Order Pattern Analysis**
Identify clusters of orders that share similar characteristics. Do certain order patterns consistently lead to delivery problems or cost overruns? What operational changes would you recommend?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of supplier risk vs. total cost. Are they the same factors, or do risk and cost depend on different aspects of the supply chain?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the VP of Operations. Include: (a) three key supply chain vulnerabilities, (b) two specific sourcing or logistics recommendations, and (c) a supplier data collection improvement plan.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
