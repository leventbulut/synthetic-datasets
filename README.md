# 📊 Synthetic Datasets for Data Science Education

A curated collection of **10 realistic synthetic datasets** spanning Healthcare, Finance, Marketing, Supply Chain, Manufacturing, Retail, Telecommunications, Education, Transportation, and Energy.

Each dataset is purpose-built for classroom use — designed with realistic feature relationships, data quality challenges, and both classification and regression targets.

---

## Getting Started

1. **Pick a dataset** from the table below
2. **Read the data dictionary** in `documentation/data_dictionaries/`
3. **Review the analytical questions** in `documentation/suggested_tasks/`
4. **Load the CSV** and start exploring

```python
import pandas as pd
df = pd.read_csv("datasets/marketing/synthetic_marketing_20250901.csv")
df.head()
```

---

## Available Datasets

| Industry | Records | Columns | Classification Target | Regression Target |
|----------|--------:|--------:|----------------------|-------------------|
| 🏥 Healthcare | 500K | 22 | Readmission risk | Total cost |
| 💰 Finance | 750K | 24 | Credit risk | Fraud risk score |
| 📈 Marketing | 600K | 29 | Churn risk | Customer lifetime value |
| 🚚 Supply Chain | 1M | 24 | Supplier risk | Total cost |
| 🏭 Manufacturing | 400K | 22 | Quality level | Production cost |
| 🛒 Retail | 800K | 24 | Customer segment | Customer lifetime value |
| 📱 Telecommunications | 550K | 22 | Churn prediction | Satisfaction score |
| 🎓 Education | 300K | 22 | Academic performance | College readiness |
| 🚗 Transportation | 450K | 22 | Delivery success | Delivery cost |
| ⚡ Energy | 350K | 22 | Efficiency level | Energy consumption |

---

## Documentation

| Folder | Contents |
|--------|----------|
| `documentation/data_dictionaries/` | Column names, data types, descriptions, units |
| `documentation/suggested_tasks/` | Analytical questions and team project scenarios |

---

## Data Quality

Every dataset contains realistic data quality challenges:

- **Missing values** — Not missing at random (MNAR); follow realistic patterns
- **Outliers** — Extreme but plausible values that require investigation
- **Entry errors** — Data-entry mistakes that must be identified and handled
- **Multiple feature types** — Numerical, categorical, and datetime columns

Plan your data-cleaning strategy **before** you start modeling.

---

## License

All datasets are synthetic — no real-world PII or proprietary data. Use freely for educational and research purposes.

MIT License — see [LICENSE](LICENSE).
