# Retail Dataset — Analytical Questions

Use the Retail dataset (`synthetic_retail_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a retail analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find? How would you handle negative values in days_since_last_visit or extreme basket sizes? Propose and justify a cleaning pipeline.

**Q2. Customer and Store Profiling**
The merchandising team wants to understand shopping patterns. Using EDA, describe how demographics, store formats, product preferences, and loyalty behavior interact. What customer archetypes emerge?

---

## 📊 Classification Challenges

**Q3. Customer Segment Prediction**
Build a classification model to predict `customer_segment` (Budget/Moderate/Premium/VIP). What distinguishes each segment? How should store managers personalize service based on predicted segments?

**Q4. Model Comparison**
Compare at least three classification algorithms. For a 4-class problem, simple accuracy can be misleading. Evaluate per-class performance and discuss which segments are easiest and hardest to identify.

**Q5. Channel and Loyalty Analysis**
Investigate whether segment membership is influenced by loyalty program participation and online purchase behavior. Should the loyalty program be redesigned to encourage upgrades from Moderate to Premium?

---

## 📈 Regression Challenges

**Q6. Customer Lifetime Value Prediction**
The CFO wants CLV estimates for customer acquisition budgeting. Build a regression model for `customer_lifetime_value`, identify the strongest value drivers, and recommend strategies to increase CLV.

**Q7. Feature Engineering**
Can you improve your CLV model with new features? Consider spending-per-visit, recency-frequency-monetary (RFM) scores, or loyalty engagement ratios. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Natural Customer Segmentation**
Ignoring the provided segment labels, use clustering to discover natural customer groups. How do your data-driven segments compare to the existing classification? Which approach reveals more actionable insights?

**Q9. Market Basket Insights**
Analyze which product categories tend to be purchased together and whether purchase patterns differ across store types. What cross-selling or visual merchandising strategies would you recommend?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the factors driving customer segmentation vs. CLV. Are high-value customers always in the VIP segment? What insights emerge from the overlap — or lack thereof?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the VP of Retail. Include: (a) three key findings about customer behavior, (b) two specific strategies to grow the VIP segment, and (c) a recommendation for improving customer data collection.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
