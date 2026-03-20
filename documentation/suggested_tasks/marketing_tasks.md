# Marketing Dataset — Analytical Questions

Use the Marketing dataset (`synthetic_marketing_20250901.csv`) to explore the scenarios below. Each question presents a realistic business problem that a marketing analytics team would face. Your task is to determine the best analytical approach, identify relevant features, build and evaluate models, and communicate actionable insights.

---

## 🔍 Exploratory Analysis

**Q1. Data Quality Audit**
Before any modeling, conduct a thorough data quality assessment. What types of issues do you find? How prevalent are they? Propose a data-cleaning pipeline and justify your choices (e.g., drop vs. impute, outlier treatment strategy).

**Q2. Customer Profile Discovery**
The CMO wants to understand "who our customers are." Using exploratory data analysis and visualization, describe the customer base. Are there natural groupings? What patterns emerge across demographics, engagement, and purchase behavior?

---

## 📊 Classification Challenges

**Q3. Churn Risk Prediction**
The VP of Customer Retention needs a model to predict which customers are at risk of churning (`churn_risk`). Build a classification model, evaluate its performance, and present the top factors driving churn risk. How would you recommend the retention team prioritize their outreach?

**Q4. Model Comparison**
Compare at least three different classification algorithms on the churn prediction task. Which model performs best, and why? Consider accuracy, interpretability, and computational cost in your recommendation.

**Q5. Class Imbalance**
Examine the distribution of the churn risk classes. Is there an imbalance? If so, how does it affect model performance? Experiment with at least two strategies to address it and report the impact.

---

## 📈 Regression Challenges

**Q6. Customer Lifetime Value Prediction**
The Finance team wants to forecast `customer_lifetime_value` for resource allocation. Build a regression model, report its accuracy (RMSE, MAE, R²), and identify the most important predictors. What business actions would you recommend based on your findings?

**Q7. Feature Engineering**
Can you improve your CLV model by creating new features? Consider ratios, interactions, polynomial terms, or temporal features derived from existing columns. Report the before/after model performance.

---

## 🧩 Unsupervised Learning

**Q8. Customer Segmentation**
Marketing wants to design targeted campaigns for distinct customer groups. Using clustering techniques, identify meaningful customer segments. How many segments do you recommend, and how would you describe each one to a non-technical stakeholder?

**Q9. Segment-Based Modeling**
After identifying customer segments (Q8), build separate churn-prediction models for each segment. Does a segment-specific approach outperform a single global model? Why or why not?

---

## 🎯 Advanced Analytics

**Q10. Feature Importance Deep Dive**
Using model-agnostic interpretability tools (e.g., SHAP, permutation importance), analyze which features matter most for both churn risk and CLV. Are the drivers the same for both targets, or do they differ? Present your findings visually.

**Q11. Actionable Recommendations**
Based on all your analyses, prepare a one-page executive summary for the CMO. Include: (a) the three most critical findings, (b) two specific campaign recommendations, and (c) a data quality improvement plan.

---

> **Note:** There is no single "correct" answer to these questions. The quality of your analysis, your reasoning about modeling choices, and the clarity of your communication are what matter most.
