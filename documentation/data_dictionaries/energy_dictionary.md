# Energy Dataset Data Dictionary

## Overview
This dataset contains 350,000 synthetic energy consumption records for energy & utilities analysis, including building efficiency, consumption patterns, environmental factors, and energy optimization.

## Column Descriptions

### Building Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| building_id | int64 | Unique building identifier | - | 0.00% |
| building_type | category | Type of building (Residential, Commercial, Industrial) | - | 0.00% |
| building_age | int64 | Age of building in years | years | 0.00% |
| building_size | float64 | Building size in square feet | sq ft | 0.00% |
| floor_count | int64 | Number of floors | count | 0.00% |
| occupancy_type | category | Type of occupancy (Full-time, Part-time, Seasonal) | - | 0.00% |

### Energy Systems
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| hvac_system_type | category | Type of HVAC system | - | 0.00% |
| hvac_efficiency_rating | float64 | HVAC system efficiency rating | SEER | 0.00% |
| lighting_system | category | Type of lighting system | - | 0.00% |
| lighting_efficiency | float64 | Lighting efficiency rating | lumens/watt | 0.00% |
| insulation_rating | category | Building insulation rating | - | 0.00% |
| window_efficiency | category | Window energy efficiency rating | - | 0.00% |

### Environmental Conditions
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| outdoor_temperature | float64 | Outdoor temperature | Fahrenheit | 0.00% |
| humidity_level | float64 | Outdoor humidity level | percentage | 0.00% |
| solar_radiation | float64 | Solar radiation intensity | W/m² | 0.00% |
| wind_speed | float64 | Wind speed | mph | 0.00% |
| precipitation | float64 | Precipitation amount | inches | 0.00% |
| cloud_cover | category | Cloud cover conditions | - | 0.00% |

### Energy Consumption
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| electricity_consumption | float64 | Monthly electricity consumption | kWh | 0.00% |
| gas_consumption | float64 | Monthly natural gas consumption | therms | 0.00% |
| water_consumption | float64 | Monthly water consumption | gallons | 0.00% |
| total_energy_consumption | float64 | Total energy consumption | BTU | 0.00% |
| peak_demand | float64 | Peak electricity demand | kW | 0.00% |
| base_load | float64 | Base electricity load | kW | 0.00% |

### Efficiency Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| energy_intensity | float64 | Energy consumption per square foot | BTU/sq ft | 0.00% |
| efficiency_score | float64 | Overall energy efficiency score | score | 0.00% |
| carbon_footprint | float64 | Carbon emissions from energy use | CO2 lbs | 0.00% |
| renewable_energy_usage | float64 | Percentage of renewable energy used | percentage | 0.00% |
| energy_star_rating | category | Energy Star certification level | - | 0.00% |
| sustainability_score | float64 | Overall sustainability rating | score | 0.00% |

### Operational Factors
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| operating_hours | float64 | Building operating hours per day | hours | 0.00% |
| occupancy_rate | float64 | Building occupancy rate | percentage | 0.00% |
| maintenance_schedule | category | Maintenance schedule frequency | - | 0.00% |
| equipment_age | float64 | Average equipment age in years | years | 0.00% |
| automation_level | category | Building automation level | - | 0.00% |
| smart_technology | category | Smart technology implementation | - | 0.00% |

### Cost Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| electricity_cost | float64 | Monthly electricity cost | USD | 0.00% |
| gas_cost | float64 | Monthly natural gas cost | USD | 0.00% |
| water_cost | float64 | Monthly water cost | USD | 0.00% |
| total_energy_cost | float64 | Total monthly energy cost | USD | 0.00% |
| cost_per_sqft | float64 | Energy cost per square foot | USD/sq ft | 0.00% |
| cost_variance | float64 | Cost variance from budget | USD | 0.00% |

### Temporal Features
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| measurement_date | datetime64[ns] | Date of energy measurement | date | 0.00% |
| season | category | Season of measurement | - | 0.00% |
| month | int64 | Month of measurement | month | 0.00% |
| day_of_week | category | Day of week | - | 0.00% |
| hour_of_day | int64 | Hour of measurement | hour | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| efficiency_level | category | Energy efficiency classification (Low, Medium, High, Excellent) | - | 0.00% |
| energy_consumption | float64 | Total energy consumption in BTU | BTU | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `efficiency_score` for older buildings
- **Business Logic**: Older buildings may not have complete efficiency assessments

### Outliers (0.2%)
- **Consumption Outliers**: Extremely high consumption (>100,000 kWh) or negative values
- **Temperature Outliers**: Unrealistic temperatures (<-50°F or >150°F)
- **Cost Outliers**: Very high costs (>$10,000) or negative costs
- **Efficiency Outliers**: Efficiency scores >100% or negative values

### Entry Errors (≤30%)
- **Consumption Errors**: Some buildings show impossible consumption patterns
- **Date Errors**: Future measurement dates or impossible sequences
- **Cost Errors**: Negative costs or inconsistent calculations
- **Building Errors**: Inconsistent building characteristics

## Target Variable Dependencies

### Efficiency Level (Classification)
Depends on:
1. **energy_intensity** - Primary predictor (negative correlation)
2. **efficiency_score** - Higher scores indicate better efficiency
3. **hvac_efficiency_rating** - Better HVAC systems improve efficiency
4. **insulation_rating** - Better insulation improves efficiency
5. **building_age** - Newer buildings tend to be more efficient
6. **renewable_energy_usage** - Higher renewable usage improves efficiency

### Energy Consumption (Regression)
Depends on:
1. **building_size** - Primary predictor (positive correlation)
2. **outdoor_temperature** - Extreme temperatures increase consumption
3. **occupancy_rate** - Higher occupancy increases consumption
4. **operating_hours** - Longer hours increase consumption
5. **building_age** - Older buildings may consume more energy
6. **efficiency_score** - Lower efficiency increases consumption
