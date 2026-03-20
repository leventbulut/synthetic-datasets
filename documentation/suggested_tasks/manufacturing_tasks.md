# Manufacturing Dataset — Analytical Questions

Use the Manufacturing dataset (`synthetic_manufacturing_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a production analytics team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find? How would you handle missing sensor readings (temperature, vibration) differently from missing quality metrics? Propose and justify a cleaning strategy.

**Q2. Production Landscape**
The plant manager wants to understand production performance across lines and shifts. Using EDA, describe how machine parameters, environmental conditions, and operator factors relate to quality and cost outcomes. What patterns emerge?

---

## 📊 Classification Challenges

**Q3. Quality Level Prediction**
Build a classification model to predict `quality_level` (High/Medium/Low). Which process parameters are most important? What thresholds would you recommend for real-time monitoring alerts?

**Q4. Model Comparison**
Compare at least three classification approaches. In manufacturing, catching a Low-quality batch before shipping is critical. How does prioritizing recall for the Low class affect overall model design?

**Q5. Shift and Machine Effects**
Investigate whether quality outcomes vary by shift (Day/Evening/Night) and machine age. Is there an interaction between operator experience and machine condition? What staffing recommendations would you make?

---

## 📈 Regression Challenges

**Q6. Production Cost Estimation**
The finance team needs per-batch cost predictions for pricing decisions. Build a regression model for `production_cost` and identify the main cost drivers. Where should the operations team focus to reduce costs without compromising quality?

**Q7. Feature Engineering**
Can you improve your cost model with engineered features? Consider ratios (defect_rate × batch_size for total defects), interactions (machine_age × vibration_level), or efficiency metrics (cost per unit). Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Production Regime Discovery**
Use clustering to identify distinct "production regimes" — combinations of conditions that tend to occur together. How many regimes exist? Which ones produce the best quality at the lowest cost?

**Q9. Anomaly Detection for Predictive Maintenance**
Can unsupervised anomaly detection flag batches produced under abnormal conditions before quality problems manifest? Compare your anomaly flags to actual quality outcomes.

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of quality level vs. production cost. Do the same factors control both, or are quality and cost driven by different process levers?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the plant manager. Include: (a) three key findings about quality drivers, (b) two specific process improvement recommendations, and (c) a sensor data collection improvement plan.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
