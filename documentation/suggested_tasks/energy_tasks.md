# Energy Dataset — Analytical Questions

Use the Energy dataset (`synthetic_energy_20250901.csv`) to explore the scenarios below. Each question presents a realistic problem that a building energy management team would face.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Conduct a thorough data quality assessment. What issues do you find (e.g., impossible building ages, extreme appliance counts)? How would you handle missing insulation data vs. missing weather readings? Propose a cleaning strategy.

**Q2. Building Portfolio Overview**
The facilities director wants to understand the building portfolio. Using EDA, describe how building characteristics, equipment age, weather exposure, and energy usage patterns vary across building types (Residential/Commercial/Industrial/Institutional). What stands out?

---

## 📊 Classification Challenges

**Q3. Efficiency Level Prediction**
Build a classification model to predict `efficiency_level` (High/Medium/Low). Which building characteristics are most predictive? How should a facilities manager prioritize retrofit investments based on your model?

**Q4. Model Comparison**
Compare at least three classification approaches. Discuss which model would be most useful for a non-technical building manager who needs to justify upgrade budgets — is interpretability more important than raw accuracy here?

**Q5. Building Type Differences**
Investigate whether efficiency drivers differ between building types. Does a residential building need a different improvement strategy than a commercial one? Build type-specific models and compare.

---

## 📈 Regression Challenges

**Q6. Energy Consumption Prediction**
The utility company wants to predict `energy_consumption_kwh` for demand planning. Build a regression model, identify the main consumption drivers, and recommend how building operators should adjust operations during extreme weather.

**Q7. Feature Engineering**
Can you improve your consumption model with new features? Consider climate-adjusted metrics (heating/cooling degree deviation from 20°C), equipment efficiency ratios (HVAC age × insulation), or solar offset calculations. Report the improvement.

---

## 🧩 Unsupervised Learning

**Q8. Building Archetypes**
Use clustering to identify natural building archetypes based on their physical characteristics and energy profiles. How many archetypes exist? Which ones represent the best candidates for energy efficiency programs?

**Q9. Weather Sensitivity Analysis**
Cluster buildings by how sensitive their energy consumption is to weather conditions. Which building features make a building more or less weather-sensitive? What design recommendations follow?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using SHAP or permutation importance, compare the drivers of efficiency level vs. energy consumption. Can a building consume a lot of energy and still be "efficient"? What does your analysis reveal about the difference between absolute consumption and efficiency?

**Q11. Actionable Recommendations**
Prepare a one-page executive summary for the sustainability committee. Include: (a) three key findings about energy efficiency drivers, (b) two specific building upgrade recommendations, and (c) a plan for a targeted solar incentive program.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
