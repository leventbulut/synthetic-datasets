# Marketing Dataset Data Dictionary

## Overview
This dataset contains 600,000 synthetic customer records for digital marketing analysis, including customer engagement, behavior patterns, and lifetime value prediction.

## Column Descriptions

### Customer Demographics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_id | int64 | Unique customer identifier | - | 0% |
| age | int64 | Customer age in years | years | 0% |
| gender | category | Customer gender (Male, Female, Other) | - | 0% |
| location | category | Geographic location (Urban, Suburban, Rural) | - | 0% |
| income_level | category | Income category (Low, Medium, High, Very High) | - | 0% |
| education_level | category | Education attainment (High School, Bachelor, Master, PhD) | - | 0% |

### Engagement Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| website_visits | int64 | Total website visits in last 30 days | count | 0% |
| app_usage_hours | float64 | Mobile app usage time in hours | hours | 0% |
| email_opens | int64 | Number of emails opened in last 30 days | count | 0% |
| email_clicks | int64 | Number of email clicks in last 30 days | count | 0% |
| social_media_engagement | float64 | Social media interaction score | score | 0% |
| newsletter_subscription | category | Newsletter subscription status | - | 0% |

### Behavioral Patterns
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| purchase_frequency | int64 | Number of purchases in last 6 months | count | 0% |
| avg_order_value | float64 | Average order value across purchases | USD | 0% |
| last_purchase_days | int64 | Days since last purchase | days | 0% |
| preferred_category | category | Most purchased product category | - | 0% |
| customer_support_contacts | int64 | Number of support contacts in last 6 months | count | 0% |
| satisfaction_score | float64 | Customer satisfaction rating | score | 0% |

### Marketing Campaign Data
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| campaign_exposure | int64 | Number of marketing campaigns exposed to | count | 0% |
| campaign_response_rate | float64 | Response rate to marketing campaigns | percentage | 0% |
| discount_usage | int64 | Number of discount codes used | count | 0% |
| referral_count | int64 | Number of customers referred | count | 0% |
| loyalty_program_tier | category | Loyalty program membership level | - | 0% |

### Temporal Features
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_since | datetime64[ns] | Date customer first registered | date | 0% |
| last_activity_date | datetime64[ns] | Date of last customer activity | date | 0% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| churn_risk | category | Customer churn risk level (Low, Medium, High) | - | 0% |
| customer_lifetime_value | float64 | Predicted customer lifetime value | USD | 0% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `satisfaction_score` for customers with low engagement
- **Business Logic**: Less engaged customers may not provide feedback

### Outliers (0.2%)
- **Engagement Outliers**: Extremely high website visits (>100/day) or app usage (>24 hours/day)
- **Purchase Outliers**: Very high order values (>$10k) or purchase frequencies (>100/month)
- **Age Outliers**: Unrealistic ages (<13 or >100)

### Entry Errors (≤30%)
- **Engagement Errors**: Some customers show impossible usage patterns
- **Date Errors**: Future dates in customer_since field
- **Value Errors**: Negative values in count fields

## Target Variable Dependencies

### Churn Risk (Classification)
Depends on:
1. **last_purchase_days** - Primary predictor (negative correlation)
2. **website_visits** - Low engagement increases churn risk
3. **app_usage_hours** - Reduced app usage indicates churn risk
4. **satisfaction_score** - Low satisfaction increases churn risk
5. **customer_support_contacts** - High support needs may indicate dissatisfaction
6. **email_engagement** - Low email interaction suggests disengagement

### Customer Lifetime Value (Regression)
Depends on:
1. **avg_order_value** - Higher order values increase CLV
2. **purchase_frequency** - More frequent purchases increase CLV
3. **income_level** - Higher income associated with higher CLV
4. **loyalty_program_tier** - Higher tiers indicate higher CLV
5. **referral_count** - Referrals suggest high-value customers
6. **campaign_response_rate** - Responsive customers tend to have higher CLV

## Data Generation Notes
- **Seed**: Randomized for novelty
- **Distributions**: Realistic marketing industry patterns
- **Seasonality**: None (static snapshot)
- **Correlations**: Maintains realistic customer behavior relationships

