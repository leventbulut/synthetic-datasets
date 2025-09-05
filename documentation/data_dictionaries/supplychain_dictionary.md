# Supply Chain Dataset Data Dictionary

## Overview
This dataset contains 1,000,000 synthetic transaction records for supply chain analysis, including supplier performance, quality metrics, cost analysis, and risk assessment.

## Column Descriptions

### Transaction Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| transaction_id | int64 | Unique transaction identifier | - | 0.00% |
| supplier_id | int64 | Unique supplier identifier | - | 0.00% |
| product_id | int64 | Unique product identifier | - | 0.00% |
| order_date | datetime64[ns] | Date when order was placed | date | 0.00% |
| delivery_date | datetime64[ns] | Actual delivery date | date | 0.00% |
| order_quantity | int64 | Quantity ordered | units | 0.00% |

### Supplier Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| supplier_name | category | Supplier company name | - | 0.00% |
| supplier_location | category | Geographic location of supplier | - | 0.00% |
| supplier_rating | float64 | Supplier performance rating | score | 0.00% |
| supplier_category | category | Supplier type (Manufacturer, Distributor, etc.) | - | 0.00% |
| years_in_business | int64 | Number of years supplier has been in business | years | 0.00% |
| certification_status | category | Quality certification status | - | 0.00% |

### Product Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| product_name | category | Product description | - | 0.00% |
| product_category | category | Product classification | - | 0.00% |
| unit_price | float64 | Price per unit | USD | 0.00% |
| product_quality_grade | category | Product quality classification | - | 0.00% |
| lead_time_days | int64 | Standard lead time for product | days | 0.00% |

### Quality Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| defect_rate | float64 | Percentage of defective items | percentage | 0.00% |
| quality_inspection_score | float64 | Quality inspection rating | score | 0.00% |
| return_rate | float64 | Percentage of items returned | percentage | 0.00% |
| customer_satisfaction_score | float64 | Customer satisfaction rating | score | 0.00% |

### Cost and Performance
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| total_cost | float64 | Total transaction cost | USD | 0.00% |
| shipping_cost | float64 | Shipping and handling cost | USD | 0.00% |
| handling_cost | float64 | Material handling cost | USD | 0.00% |
| on_time_delivery | category | Whether delivery was on time | - | 0.00% |
| delivery_performance_score | float64 | Delivery performance rating | score | 0.00% |

### Risk and Compliance
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| compliance_score | float64 | Regulatory compliance rating | score | 0.00% |
| risk_assessment_score | float64 | Overall risk assessment | score | 0.00% |
| insurance_coverage | category | Insurance coverage level | - | 0.00% |
| contract_terms | category | Contract terms and conditions | - | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| supplier_risk_level | category | Supplier risk classification (Low, Medium, High, Critical) | - | 0.00% |
| total_cost | float64 | Total transaction cost including all expenses | USD | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `quality_inspection_score` for low-value transactions
- **Business Logic**: Smaller orders may not undergo full quality inspection

### Outliers (0.2%)
- **Cost Outliers**: Extremely high unit prices (>$10k) or order quantities (>100k units)
- **Quality Outliers**: Perfect quality scores (100%) or extremely low scores (<10%)
- **Lead Time Outliers**: Negative lead times or extremely long lead times (>365 days)

### Entry Errors (≤30%)
- **Date Errors**: Some delivery dates before order dates
- **Quantity Errors**: Negative order quantities or unrealistic values
- **Cost Errors**: Negative costs or inconsistent pricing

## Target Variable Dependencies

### Supplier Risk Level (Classification)
Depends on:
1. **defect_rate** - Primary predictor (positive correlation with risk)
2. **delivery_performance_score** - Poor delivery performance increases risk
3. **compliance_score** - Low compliance increases risk
4. **return_rate** - High return rates indicate risk
5. **supplier_rating** - Low supplier ratings increase risk
6. **years_in_business** - Newer suppliers may have higher risk

### Total Cost (Regression)
Depends on:
1. **unit_price** - Primary cost driver
2. **order_quantity** - Higher quantities affect total cost
3. **shipping_cost** - Distance and delivery method impact
4. **handling_cost** - Product characteristics affect handling
5. **supplier_location** - Geographic factors influence costs
6. **product_quality_grade** - Higher quality may command premium pricing
