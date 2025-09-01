# Telecommunications Dataset Data Dictionary

## Overview
This dataset contains 550,000 synthetic customer records for telecommunications analysis, including service usage, customer behavior, churn prediction, and satisfaction analysis.

## Column Descriptions

### Customer Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_id | int64 | Unique customer identifier | - | 0% |
| customer_age | int64 | Customer age in years | years | 0% |
| customer_gender | category | Customer gender (Male, Female, Other) | - | 0% |
| customer_location | category | Geographic location (Urban, Suburban, Rural) | - | 0% |
| income_level | category | Income category (Low, Medium, High, Very High) | - | 0% |
| education_level | category | Education attainment (High School, Bachelor, Master, PhD) | - | 0% |

### Service Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| service_type | category | Type of service (Mobile, Internet, TV, Bundle) | - | 0% |
| plan_type | category | Service plan category (Basic, Standard, Premium, Unlimited) | - | 0% |
| contract_length | int64 | Contract duration in months | months | 0% |
| monthly_charge | float64 | Monthly service charge | USD | 0% |
| total_charges | float64 | Total charges to date | USD | 0% |
| service_start_date | datetime64[ns] | Date service was activated | date | 0% |

### Usage Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| voice_minutes | float64 | Monthly voice call minutes | minutes | 0% |
| data_usage_gb | float64 | Monthly data usage in GB | GB | 0% |
| text_messages | int64 | Monthly text messages sent | count | 0% |
| video_streaming_hours | float64 | Monthly video streaming hours | hours | 0% |
| international_calls | int64 | Monthly international calls | count | 0% |
| roaming_usage | float64 | Monthly roaming data usage | GB | 0% |

### Customer Behavior
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_service_calls | int64 | Number of customer service calls | count | 0% |
| technical_support_calls | int64 | Number of technical support calls | count | 0% |
| billing_queries | int64 | Number of billing-related queries | count | 0% |
| complaint_count | int64 | Number of complaints filed | count | 0% |
| upgrade_requests | int64 | Number of service upgrade requests | count | 0% |
| downgrade_requests | int64 | Number of service downgrade requests | count | 0% |

### Service Quality
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| network_coverage_score | float64 | Network coverage quality rating | score | 0% |
| call_drop_rate | float64 | Percentage of dropped calls | percentage | 0% |
| data_speed_score | float64 | Data speed performance rating | score | 0% |
| service_reliability | float64 | Overall service reliability score | score | 0% |
| outage_frequency | int64 | Number of service outages experienced | count | 0% |
| resolution_time_hours | float64 | Average issue resolution time | hours | 0% |

### Billing and Payment
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| payment_method | category | Payment method used | - | 0% |
| paperless_billing | category | Whether paperless billing is enabled | - | 0% |
| auto_pay_enabled | category | Whether automatic payment is enabled | - | 0% |
| late_payment_count | int64 | Number of late payments | count | 0% |
| payment_delay_days | int64 | Average payment delay in days | days | 0% |
| billing_accuracy_score | float64 | Billing accuracy rating | score | 0% |

### Customer Relationship
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_since | datetime64[ns] | Date customer first subscribed | date | 0% |
| loyalty_program_tier | category | Loyalty program membership level | - | 0% |
| referral_count | int64 | Number of customers referred | count | 0% |
| social_media_engagement | category | Social media engagement level | - | 0% |
| app_usage_frequency | category | Mobile app usage frequency | - | 0% |
| online_account_usage | category | Online account usage level | - | 0% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| customer_churn | category | Customer churn status (Churned, Retained) | - | 0% |
| satisfaction_score | float64 | Customer satisfaction rating | score | 0% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `satisfaction_score` for customers with low usage
- **Business Logic**: Low-usage customers may not provide satisfaction feedback

### Outliers (0.2%)
- **Usage Outliers**: Extremely high data usage (>1000 GB) or voice minutes (>10000)
- **Age Outliers**: Unrealistic customer ages (<13 or >100)
- **Cost Outliers**: Very high monthly charges (>$500) or negative values
- **Score Outliers**: Perfect scores (10.0) or extremely low scores (<1.0)

### Entry Errors (≤30%)
- **Usage Errors**: Some customers show impossible usage patterns
- **Date Errors**: Future service start dates or impossible sequences
- **Cost Errors**: Negative charges or inconsistent pricing
- **Behavior Errors**: Inconsistent customer behavior patterns

## Target Variable Dependencies

### Customer Churn (Classification)
Depends on:
1. **customer_service_calls** - Primary predictor (positive correlation with churn)
2. **complaint_count** - Higher complaints increase churn risk
3. **satisfaction_score** - Lower satisfaction increases churn risk
4. **call_drop_rate** - Poor network quality increases churn risk
5. **resolution_time_hours** - Longer resolution times increase churn risk
6. **late_payment_count** - Payment issues indicate churn risk

### Satisfaction Score (Regression)
Depends on:
1. **network_coverage_score** - Better coverage improves satisfaction
2. **data_speed_score** - Faster speeds increase satisfaction
3. **service_reliability** - More reliable service improves satisfaction
4. **billing_accuracy_score** - Accurate billing increases satisfaction
5. **resolution_time_hours** - Faster issue resolution improves satisfaction
6. **customer_service_calls** - Fewer service calls indicate higher satisfaction

## Data Generation Notes
- **Seed**: Randomized for novelty
- **Distributions**: Realistic telecommunications industry patterns
- **Seasonality**: None (static snapshot)
- **Correlations**: Maintains realistic telecom relationships

