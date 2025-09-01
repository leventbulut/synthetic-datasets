# Transportation Dataset Data Dictionary

## Overview
This dataset contains 450,000 synthetic delivery records for transportation analysis, including delivery performance, route optimization, cost analysis, and success prediction.

## Column Descriptions

### Delivery Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| delivery_id | int64 | Unique delivery identifier | - | 0% |
| order_id | int64 | Associated order identifier | - | 0% |
| customer_id | int64 | Customer identifier | - | 0% |
| delivery_date | datetime64[ns] | Scheduled delivery date | date | 0% |
| actual_delivery_date | datetime64[ns] | Actual delivery date | date | 0% |
| delivery_window | category | Delivery time window | - | 0% |

### Route and Location
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| origin_location | category | Origin location identifier | - | 0% |
| destination_location | category | Destination location identifier | - | 0% |
| route_distance | float64 | Route distance in miles | miles | 0% |
| estimated_travel_time | float64 | Estimated travel time in minutes | minutes | 0% |
| actual_travel_time | float64 | Actual travel time in minutes | minutes | 0% |
| route_type | category | Type of route (Highway, Local, Mixed) | - | 0% |

### Vehicle and Driver
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| vehicle_id | int64 | Vehicle identifier | - | 0% |
| driver_id | int64 | Driver identifier | - | 0% |
| vehicle_type | category | Type of vehicle (Van, Truck, Car) | - | 0% |
| vehicle_capacity | float64 | Vehicle cargo capacity | cubic feet | 0% |
| driver_experience_years | float64 | Driver experience in years | years | 0% |
| driver_rating | float64 | Driver performance rating | score | 0% |

### Package Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| package_weight | float64 | Package weight in pounds | lbs | 0% |
| package_volume | float64 | Package volume in cubic feet | cubic feet | 0% |
| package_fragility | category | Package fragility level | - | 0% |
| special_handling | category | Special handling requirements | - | 0% |
| insurance_value | float64 | Package insurance value | USD | 0% |
| delivery_priority | category | Delivery priority level | - | 0% |

### Environmental Conditions
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| weather_condition | category | Weather condition during delivery | - | 0% |
| temperature | float64 | Temperature during delivery | Fahrenheit | 0% |
| precipitation | float64 | Precipitation amount | inches | 0% |
| wind_speed | float64 | Wind speed during delivery | mph | 0% |
| visibility | float64 | Visibility conditions | miles | 0% |
| road_condition | category | Road condition rating | - | 0% |

### Performance Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| on_time_delivery | category | Whether delivery was on time | - | 0% |
| delivery_success | category | Delivery success status | - | 0% |
| customer_satisfaction | float64 | Customer satisfaction rating | score | 0% |
| delivery_accuracy | float64 | Delivery accuracy score | score | 0% |
| handling_quality | float64 | Package handling quality rating | score | 0% |
| communication_quality | float64 | Communication quality rating | score | 0% |

### Cost Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| fuel_cost | float64 | Fuel cost for delivery | USD | 0% |
| labor_cost | float64 | Labor cost for delivery | USD | 0% |
| vehicle_maintenance_cost | float64 | Vehicle maintenance cost | USD | 0% |
| insurance_cost | float64 | Insurance cost for delivery | USD | 0% |
| total_delivery_cost | float64 | Total delivery cost | USD | 0% |
| cost_per_mile | float64 | Cost per mile traveled | USD/mile | 0% |

### Operational Factors
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| traffic_conditions | category | Traffic condition rating | - | 0% |
| peak_hour_delivery | category | Whether delivery is during peak hours | - | 0% |
| weekend_delivery | category | Whether delivery is on weekend | - | 0% |
| holiday_delivery | category | Whether delivery is on holiday | - | 0% |
| seasonal_factor | category | Seasonal delivery factor | - | 0% |
| special_events | category | Special events affecting delivery | - | 0% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| delivery_success | category | Delivery success classification (Successful, Failed, Delayed) | - | 0% |
| delivery_cost | float64 | Total delivery cost including all expenses | USD | 0% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `customer_satisfaction` for failed deliveries
- **Business Logic**: Failed deliveries may not receive customer feedback

### Outliers (0.2%)
- **Distance Outliers**: Extremely long routes (>1000 miles) or negative distances
- **Cost Outliers**: Very high costs (>$1000) or negative costs
- **Time Outliers**: Negative travel times or extremely long times
- **Weight Outliers**: Extremely heavy packages (>1000 lbs) or negative weights

### Entry Errors (≤30%)
- **Date Errors**: Actual delivery dates before scheduled dates
- **Time Errors**: Negative travel times or impossible sequences
- **Cost Errors**: Negative costs or inconsistent calculations
- **Route Errors**: Impossible route combinations

## Target Variable Dependencies

### Delivery Success (Classification)
Depends on:
1. **weather_condition** - Primary predictor (adverse weather reduces success)
2. **traffic_conditions** - Poor traffic reduces success
3. **driver_rating** - Higher driver ratings improve success
4. **vehicle_condition** - Better vehicle condition improves success
5. **route_distance** - Longer routes may reduce success
6. **delivery_priority** - Higher priority improves success

### Delivery Cost (Regression)
Depends on:
1. **route_distance** - Primary cost driver
2. **fuel_cost** - Distance and fuel efficiency affect cost
3. **labor_cost** - Travel time affects labor cost
4. **vehicle_maintenance_cost** - Vehicle type and condition affect cost
5. **package_weight** - Heavier packages increase cost
6. **delivery_priority** - Priority services increase cost

## Data Generation Notes
- **Seed**: Randomized for novelty
- **Distributions**: Realistic transportation industry patterns
- **Seasonality**: None (static snapshot)
- **Correlations**: Maintains realistic transportation relationships

