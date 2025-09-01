# Synthetic Data Repository

Welcome! This repo contains **realistic synthetic datasets** for practicing data science and machine learning. All datasets are generated with sophisticated logic (seasonality, dependencies, outliers, missingness) but **contain no real-world PII or proprietary data**.

## 📂 What's Inside

- `datasets/` → Industry-organized CSV datasets (100k–2M rows)
- `documentation/` → Comprehensive guides organized by type
  - `data_dictionaries/` → Column descriptions and metadata
  - `business_contexts/` → Industry problems and impact
  - `suggested_tasks/` → Analytical problems to solve
- `INDUSTRY_INDEX.md` → Quick overview of all available datasets

## 🏭 Available Datasets

| Dataset | Industry | Size | Target Variables | Key Features |
|---------|----------|------|------------------|--------------|
| **Healthcare** | Healthcare | 500K | Readmission Risk (4-class), Total Cost (regression) | Patient demographics, vital signs, lab values, medical history |
| **Finance** | Financial Services | 750K | Credit Risk (4-class), Fraud Risk Score (regression) | Customer financials, credit history, behavioral patterns |
| **Marketing** | Digital Marketing | 600K | Churn Risk (3-class), Customer Lifetime Value (regression) | Customer engagement, purchase behavior, campaign data |
| **Supply Chain** | Supply Chain | 1M | Supplier Risk (4-class), Total Cost (regression) | Supplier performance, quality metrics, transaction data |
| **Manufacturing** | Manufacturing | 400K | Quality Grade (4-class), Production Cost (regression) | Production parameters, quality metrics, cost data |
| **Retail** | Retail | 800K | Customer Segment (4-class), Predicted CLV (regression) | Sales transactions, customer behavior, store metrics |
| **Telecommunications** | Telecom | 550K | Customer Churn (2-class), Satisfaction Score (regression) | Service usage, customer behavior, quality metrics |
| **Education** | Education | 300K | Academic Performance (4-class), College Readiness (regression) | Student demographics, academic metrics, behavioral data |
| **Transportation** | Transportation | 450K | Delivery Success (3-class), Delivery Cost (regression) | Route data, environmental conditions, performance metrics |
| **Energy** | Energy & Utilities | 350K | Efficiency Level (4-class), Energy Consumption (regression) | Building metrics, environmental data, efficiency ratings |

## 🧑‍🏫 Use Cases

- **Faculty**: Teaching regression, classification, clustering
- **Students**: Practice building models on realistic data
- **Researchers**: Test ML pipelines at scale
- **Professionals**: Validate approaches before production deployment

## ✅ Example Problems

### Classification Tasks
- Predict customer churn in marketing dataset
- Classify supplier risk levels in supply chain data
- Identify quality grades in manufacturing processes
- Segment customers in retail transactions

### Regression Tasks
- Forecast hospital readmission costs
- Predict customer lifetime value
- Estimate delivery costs in transportation
- Model energy consumption patterns

### Clustering Tasks
- Segment customers by behavior patterns
- Group suppliers by performance characteristics
- Cluster students by academic profiles
- Identify building efficiency groups

### Advanced Analytics
- Portfolio risk optimization in finance
- Supply chain disruption prediction
- Manufacturing process optimization
- Energy efficiency improvement strategies

## 🔧 Data Quality Features

Each dataset includes realistic data quality challenges:
- **Missing Values**: 3% MNAR (Missing Not At Random) patterns
- **Outliers**: 0.2% extreme values for anomaly detection practice
- **Entry Errors**: ≤30% data inconsistencies for data cleaning practice
- **Dependencies**: Targets depend on ≥5 predictors for realistic ML challenges

## 📚 Documentation Structure

### Data Dictionaries (`documentation/data_dictionaries/`)
- **Column Descriptions**: Name, type, description, units, missingness
- **Data Quality Notes**: Missingness patterns, outliers, entry errors
- **Target Dependencies**: How target variables relate to features
- **Generation Notes**: Data characteristics and patterns

### Business Context (`documentation/business_contexts/`)
- **Business Problem**: Industry challenges and use cases
- **Why Real Data Can't Be Shared**: Privacy, regulatory, competitive reasons
- **Industry Impact**: Business value and strategic importance
- **Synthetic Data Benefits**: Research and educational advantages

### Suggested Tasks (`documentation/suggested_tasks/`)
- **Analytical Objectives**: Clear problem statements and goals
- **Key Features**: Relevant variables for each task
- **Business Impact**: Real-world applications and value
- **Suggested Approaches**: ML techniques and methodologies
- **Evaluation Metrics**: Performance measurement criteria

## 🚀 Getting Started

1. **Choose a Dataset**: Select based on your industry interest or learning objectives
2. **Review Documentation**: Read the data dictionary and business context
3. **Select a Task**: Pick from suggested analytical problems
4. **Load and Explore**: Use pandas to load CSV and explore data structure
5. **Build Models**: Apply your ML skills to solve real-world problems

## 📊 Data Characteristics

- **Size Range**: 300K to 1M records for scalable learning
- **Column Count**: ≥20 columns with diverse data types
- **Feature Types**: Numerical, categorical, and datetime variables
- **Target Balance**: Classification targets are balanced, regression targets are skewed
- **Realistic Patterns**: Industry-specific distributions and relationships

## 🤝 Contributing

This repository is designed for educational and research purposes. Feel free to:
- Use datasets for coursework and research
- Share your solutions and insights
- Suggest improvements to documentation
- Report issues or inconsistencies

## 📄 License

All datasets are synthetic and contain no real-world data. Use freely for educational and research purposes.

---

**Happy Learning!** 🎓📈
