# Manufacturing Dataset Data Dictionary

## Overview
This dataset contains 400,000 synthetic production batch records for manufacturing analysis, including quality control, production efficiency, cost management, and process optimization.

## Column Descriptions

### Batch Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| batch_id | int64 | Unique batch identifier | - | 0.00% |
| product_id | int64 | Unique product identifier | - | 0.00% |
| production_line | category | Production line identifier | - | 0.00% |
| shift_type | category | Production shift (Day, Night, Weekend) | - | 0.00% |
| batch_size | int64 | Number of units in batch | units | 0.00% |

### Production Parameters
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| temperature | float64 | Production temperature | Celsius | 0.00% |
| pressure | float64 | Production pressure | PSI | 0.98% |
| humidity | float64 | Production humidity | percentage | 0.98% |
| speed | float64 | Production line speed | units/hour | 0.00% |
| material_quality | category | Raw material quality grade | - | 0.02% |
| operator_id | int64 | Production operator identifier | - | 0.00% |

### Quality Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| defect_count | int64 | Number of defective units | count | 0.00% |
| defect_rate | float64 | Percentage of defective units | percentage | 0.00% |
| quality_score | float64 | Overall quality rating | score | 0.02% |
| inspection_result | category | Quality inspection outcome | - | 0.00% |
| rework_required | category | Whether rework is needed | - | 0.00% |

### Performance Metrics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| cycle_time | float64 | Time per unit production | minutes | 0.00% |
| downtime_minutes | float64 | Production downtime duration | minutes | 0.00% |
| efficiency_score | float64 | Production efficiency rating | score | 0.02% |
| throughput | float64 | Units produced per hour | units/hour | 0.00% |
| yield_rate | float64 | Percentage of good units | percentage | 0.96% |

### Cost Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| material_cost | float64 | Raw material cost per unit | USD | 0.00% |
| labor_cost | float64 | Labor cost per unit | USD | 0.00% |
| overhead_cost | float64 | Overhead cost per unit | USD | 0.00% |
| total_cost | float64 | Total cost per unit | USD | 0.00% |
| cost_variance | float64 | Cost variance from standard | USD | 0.00% |

### Environmental Conditions
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| ambient_temperature | float64 | Ambient temperature | Celsius | 0.00% |
| air_quality | category | Air quality rating | - | 0.00% |
| noise_level | float64 | Production noise level | decibels | 0.00% |
| vibration_level | float64 | Equipment vibration level | mm/s | 0.00% |

### Temporal Features
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| start_time | datetime64[ns] | Batch production start time | datetime | 0.00% |
| completion_time | datetime64[ns] | Batch completion time | datetime | 0.00% |
| production_date | datetime64[ns] | Date of production | date | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| quality_grade | category | Final quality classification (A, B, C, D) | - | 0.00% |
| production_cost | float64 | Total production cost per unit | USD | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `quality_score` for batches with low defect rates
- **Business Logic**: High-quality batches may not require detailed quality scoring

### Outliers (0.2%)
- **Temperature Outliers**: Extremely high temperatures (>200°C) or very low temperatures (<-50°C)
- **Cost Outliers**: Very high costs (>$1000/unit) or negative costs
- **Efficiency Outliers**: Efficiency scores >100% or negative values
- **Time Outliers**: Negative cycle times or extremely long production times

### Entry Errors (≤30%)
- **Parameter Errors**: Some batches show impossible parameter combinations
- **Date Errors**: Completion times before start times
- **Cost Errors**: Inconsistent cost calculations
- **Quality Errors**: Defect counts exceeding batch sizes

## Target Variable Dependencies

### Quality Grade (Classification)
Depends on:
1. **defect_rate** - Primary predictor (negative correlation)
2. **quality_score** - Higher scores indicate better quality
3. **material_quality** - Better materials improve quality
4. **temperature** - Optimal temperature range improves quality
5. **pressure** - Proper pressure control affects quality
6. **operator_id** - Operator skill influences quality

### Production Cost (Regression)
Depends on:
1. **material_cost** - Primary cost driver
2. **labor_cost** - Labor efficiency affects cost
3. **cycle_time** - Longer cycle times increase labor cost
4. **downtime_minutes** - Downtime increases overhead cost
5. **batch_size** - Economies of scale affect unit cost
6. **efficiency_score** - Lower efficiency increases cost
