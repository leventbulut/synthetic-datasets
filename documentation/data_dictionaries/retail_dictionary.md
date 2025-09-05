# Retail Dataset Data Dictionary

## Overview
This dataset contains 800,000 synthetic sales transaction records for retail analysis, including customer behavior, product performance, sales patterns, and customer lifetime value prediction.

## Column Descriptions

### Transaction Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| transaction_id | int64 | Unique transaction identifier | - | 0.00% |
| customer_id | int64 | Unique customer identifier | - | 0.00% |
| product_id | int64 | Unique product identifier | - | 0.00% |
| transaction_date | datetime64[ns] | Date and time of transaction | datetime | 0.00% |
| store_id | int64 | Store location identifier | - | 0.00% |
| sales_channel | category | Sales channel (In-store, Online, Mobile) | - | 0.00% |

### Customer Demographics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_age | int64 | Customer age in years | years | 0.00% |
| customer_gender | category | Customer gender (Male, Female, Other) | - | 0.00% |
| customer_location | category | Geographic location (Urban, Suburban, Rural) | - | 0.00% |
| income_level | category | Income category (Low, Medium, High, Very High) | - | 0.00% |
| customer_segment | category | Customer segment (Budget, Regular, Premium, Luxury) | - | 0.00% |
| loyalty_program_tier | category | Loyalty program membership level | - | 0.00% |

### Product Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| product_name | category | Product description | - | 0.00% |
| product_category | category | Product classification | - | 0.00% |
| product_brand | category | Product brand name | - | 0.00% |
| product_price | float64 | Product unit price | USD | 0.00% |
| product_cost | float64 | Product cost to retailer | USD | 0.00% |
| product_rating | float64 | Customer product rating | score | 0.00% |

### Sales Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| quantity_sold | int64 | Number of units sold | units | 0.00% |
| unit_price | float64 | Price per unit | USD | 0.00% |
| total_amount | float64 | Total transaction amount | USD | 0.00% |
| discount_amount | float64 | Discount amount applied | USD | 0.00% |
| final_amount | float64 | Final amount after discounts | USD | 0.00% |
| profit_margin | float64 | Profit margin percentage | percentage | 0.00% |

### Customer Behavior
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| purchase_frequency | int64 | Customer purchase frequency | purchases/month | 0.00% |
| avg_order_value | float64 | Average order value | USD | 0.00% |
| last_purchase_days | int64 | Days since last purchase | days | 0.00% |
| total_purchases | int64 | Total number of purchases | count | 0.00% |
| return_history | int64 | Number of items returned | count | 0.00% |
| customer_satisfaction | float64 | Customer satisfaction score | score | 0.00% |

### Store and Channel
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| store_location | category | Store geographic location | - | 0.00% |
| store_size | category | Store size category | - | 0.00% |
| store_rating | float64 | Store customer rating | score | 0.00% |
| channel_performance | float64 | Channel performance score | score | 0.00% |
| online_experience | category | Online shopping experience | - | 0.00% |

### Temporal Features
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_since | datetime64[ns] | Date customer first registered | date | 0.00% |
| season | category | Season of transaction | - | 0.00% |
| day_of_week | category | Day of week | - | 0.00% |
| hour_of_day | int64 | Hour of transaction | hour | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_segment | category | Customer segment classification (Budget, Regular, Premium, Luxury) | - | 0.00% |
| predicted_clv | float64 | Predicted customer lifetime value | USD | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `customer_satisfaction` for low-value transactions
- **Business Logic**: Smaller transactions may not trigger satisfaction surveys

### Outliers (0.2%)
- **Price Outliers**: Extremely high prices (>$10k) or negative prices
- **Quantity Outliers**: Very high quantities (>1000 units) or negative quantities
- **Age Outliers**: Unrealistic customer ages (<13 or >100)
- **Rating Outliers**: Perfect ratings (10.0) or extremely low ratings (<1.0)

### Entry Errors (≤30%)
- **Price Errors**: Some products show inconsistent pricing
- **Date Errors**: Future transaction dates or impossible time sequences
- **Quantity Errors**: Negative quantities or unrealistic values
- **Customer Errors**: Inconsistent customer demographics

## Target Variable Dependencies

### Customer Segment (Classification)
Depends on:
1. **avg_order_value** - Primary predictor (positive correlation)
2. **purchase_frequency** - Higher frequency indicates premium segment
3. **income_level** - Higher income associated with premium segments
4. **loyalty_program_tier** - Higher tiers indicate premium customers
5. **total_purchases** - More purchases suggest higher-value segments
6. **customer_satisfaction** - Higher satisfaction associated with premium segments

### Predicted CLV (Regression)
Depends on:
1. **avg_order_value** - Higher order values increase CLV
2. **purchase_frequency** - More frequent purchases increase CLV
3. **total_purchases** - Purchase history indicates future value
4. **income_level** - Higher income associated with higher CLV
5. **loyalty_program_tier** - Higher tiers indicate higher CLV
6. **customer_satisfaction** - Satisfied customers have higher retention
