# Transportation Dataset — Analytical Questions

Use the Transportation dataset (`synthetic_transportation_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a logistics analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find (e.g., negative delay values, impossible durations)? How would you handle missing GPS-derived metrics vs. missing driver ratings? Propose a cleaning strategy.

**Q2. Operations Overview**
The fleet manager wants a comprehensive picture of delivery operations. Using EDA, describe how route types, vehicle choices, driver characteristics, and weather conditions relate to delivery outcomes and costs. What patterns emerge?

---

## 📊 Classification Challenges

**Q3. Delivery Outcome Prediction**
Build a classification model to predict `delivery_success` (On Time/Minor Delay/Major Delay). Which factors most influence on-time performance? How could dispatchers use this model to flag at-risk shipments before they leave?

**Q4. Model Comparison**
Compare at least three classification algorithms. Discuss the operational impact of misclassification — what actions should the company take when a shipment is predicted as "Major Delay"?

**Q5. Weather and Route Effects**
Investigate how weather conditions and route types interact to affect delivery outcomes. Can the company build different performance benchmarks for clear-highway vs. snow-urban deliveries?

---

## 📈 Regression Challenges

**Q6. Delivery Cost Estimation**
The pricing team needs accurate delivery cost estimates. Build a regression model for `delivery_cost`, identify the main cost drivers, and recommend where the company could reduce costs through operational changes.

**Q7. Feature Engineering**
Can you improve your cost model with new features? Consider speed metrics (distance/duration), fuel efficiency adjusted for load weight, or delay-adjusted cost per km. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Delivery Route Clustering**
Use clustering to identify distinct delivery profiles. How many exist? Which route profiles are most efficient and which are consistently problematic?

**Q9. Driver-Vehicle Matching**
Analyze whether certain driver experience levels paired with certain vehicle types deliver better outcomes. Use your analysis to recommend an optimal driver-vehicle assignment strategy.

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of delivery success vs. delivery cost. Can the company optimize for on-time performance and low cost simultaneously, or are there trade-offs?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the VP of Logistics. Include: (a) three key findings about delivery performance drivers, (b) two specific fleet or routing recommendations, and (c) a plan for improving delivery data collection.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
