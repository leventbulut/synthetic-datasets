# Healthcare Dataset Data Dictionary

## Dataset Overview
- **Total Rows**: 500,000 patient records
- **Total Columns**: 22
- **Date Range**: January 2022 - December 2023
- **Target Variables**: 2 (1 classification, 1 regression)

## Column Descriptions

### Patient Identifiers
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `patient_id` | String | Unique patient identifier | N/A | 0% |
| `admission_date` | Datetime | Date and time of hospital admission | YYYY-MM-DD | 0% |
| `discharge_date` | Datetime | Date and time of hospital discharge | YYYY-MM-DD | 0% |

### Demographics
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `age` | Integer | Patient age at admission | Years | 0% |
| `gender` | Categorical | Patient gender | M/F | 0% |

### Clinical Information
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `admission_type` | Categorical | Type of hospital admission | Emergency/Elective/Urgent/Trauma | 0% |
| `primary_diagnosis` | Categorical | Primary medical diagnosis category | Cardiovascular/Respiratory/Gastrointestinal/Neurological/Orthopedic | 0% |
| `length_of_stay` | Integer | Number of days in hospital | Days | 0% |
| `hospital_department` | Categorical | Hospital department where patient was treated | ICU/Cardiology/Emergency/General Medicine/Surgery/Pediatrics | 0% |

### Vital Signs
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `systolic_bp` | Float | Systolic blood pressure | mmHg | 1.2% |
| `diastolic_bp` | Float | Diastolic blood pressure | mmHg | 1.2% |
| `heart_rate` | Float | Heart rate | Beats per minute | 1.2% |
| `temperature` | Float | Body temperature | Fahrenheit | 0.6% |

### Laboratory Values
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `hemoglobin` | Float | Hemoglobin level | g/dL | 0.8% |
| `creatinine` | Float | Serum creatinine level | mg/dL | 0.8% |
| `glucose` | Float | Blood glucose level | mg/dL | 0.8% |

### Administrative & Clinical Counts
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `comorbidity_count` | Integer | Number of comorbid conditions | Count | 0% |
| `medication_count` | Integer | Number of medications prescribed | Count | 0% |
| `insurance_type` | Categorical | Type of health insurance | Medicare/Medicaid/Private/Self-Pay/Other | 0% |

### Target Variables
| Column Name | Type | Description | Unit | % Missing |
|-------------|------|-------------|------|-----------|
| `readmission_risk` | Integer | Classification target: Readmission risk level | 0=Low, 1=Medium, 2=High | 0% |
| `total_cost` | Float | Regression target: Total hospitalization cost | USD | 0% |

## Data Quality Notes

### Missing Values (MNAR - Missing Not At Random)
- **Overall missingness**: ~3%
- **Vital signs**: Higher missingness for emergency admissions
- **Lab values**: More likely to be missing in trauma/emergency cases

### Outliers (~0.2%)
- Impossible vital sign values (e.g., BP >300, temperature >110°F)
- These represent data entry errors or measurement artifacts

### Entry Errors (~30%)
- Pediatric ages in adult dataset
- Unrealistic length of stay values
- Excessive medication counts

## Data Dependencies

### Readmission Risk (Classification Target)
Depends on 5+ predictors:
- Age (older patients higher risk)
- Length of stay (longer stays higher risk)
- Comorbidity count (more conditions higher risk)
- Primary diagnosis (cardiovascular/neurological higher risk)
- Insurance type (Medicare/Medicaid higher risk)

### Total Cost (Regression Target)
Depends on 5+ predictors:
- Length of stay (primary driver)
- Hospital department (ICU/Surgery highest)
- Age (older patients slightly higher)
- Primary diagnosis (neurological/cardiovascular higher)
- Insurance type (private insurance higher)

## Clinical Context
This dataset represents a realistic hospital population with:
- Typical age distribution (mean ~65 years)
- Realistic vital sign ranges and correlations
- Appropriate length of stay distributions
- Realistic cost structures by department and diagnosis
- Seasonal admission patterns over 2 years
