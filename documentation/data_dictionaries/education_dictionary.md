# Education Dataset Data Dictionary

## Overview
This dataset contains 300,000 synthetic student records for educational analysis, including academic performance, demographic factors, learning behaviors, and college readiness assessment.

## Column Descriptions

### Student Demographics
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| student_id | int64 | Unique student identifier | - | 0.00% |
| student_age | int64 | Student age in years | years | 0.00% |
| student_gender | category | Student gender (Male, Female, Other) | - | 0.00% |
| ethnicity | category | Student ethnicity | - | 0.00% |
| family_income | category | Family income level (Low, Medium, High, Very High) | - | 0.09% |
| parent_education | category | Highest parent education level | - | 0.09% |

### Academic Information
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| grade_level | int64 | Current grade level (9-12) | grade | 0.00% |
| school_type | category | Type of school (Public, Private, Charter) | - | 0.00% |
| school_rating | float64 | School performance rating | score | 0.00% |
| class_size | int64 | Average class size | students | 0.00% |
| teacher_experience | float64 | Average teacher experience in years | years | 0.00% |
| curriculum_type | category | Type of curriculum (Standard, Advanced, IB, AP) | - | 0.00% |

### Academic Performance
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| gpa | float64 | Grade Point Average | score | 0.00% |
| math_score | float64 | Mathematics standardized test score | score | 0.00% |
| reading_score | float64 | Reading standardized test score | score | 0.00% |
| science_score | float64 | Science standardized test score | score | 0.00% |
| writing_score | float64 | Writing standardized test score | score | 0.00% |
| overall_academic_score | float64 | Composite academic performance score | score | 0.00% |

### Learning Behaviors
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| study_hours_per_week | float64 | Hours spent studying per week | hours | 0.79% |
| homework_completion_rate | float64 | Percentage of homework completed | percentage | 0.91% |
| class_attendance_rate | float64 | Percentage of classes attended | percentage | 0.00% |
| participation_score | float64 | Class participation rating | score | 0.00% |
| time_management_score | float64 | Time management skills rating | score | 0.00% |
| organization_score | float64 | Organizational skills rating | score | 0.00% |

### Extracurricular Activities
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| sports_participation | category | Sports participation level | - | 0.00% |
| club_membership | int64 | Number of clubs/organizations joined | count | 0.82% |
| leadership_roles | int64 | Number of leadership positions held | count | 0.00% |
| community_service_hours | float64 | Community service hours completed | hours | 0.00% |
| artistic_activities | category | Participation in artistic activities | - | 0.00% |
| technology_engagement | category | Technology and coding engagement | - | 0.00% |

### Social and Emotional Factors
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| peer_relationships | float64 | Peer relationship quality score | score | 0.00% |
| teacher_relationships | float64 | Teacher relationship quality score | score | 0.00% |
| self_confidence_score | float64 | Self-confidence assessment score | score | 0.00% |
| stress_level | category | Perceived stress level | - | 0.00% |
| motivation_score | float64 | Academic motivation rating | score | 0.00% |
| resilience_score | float64 | Resilience and coping skills rating | score | 0.00% |

### Family and Support
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| family_support_score | float64 | Family support for education rating | score | 0.00% |
| parent_involvement | category | Level of parent involvement in education | - | 0.00% |
| tutoring_received | category | Whether student receives tutoring | - | 0.00% |
| learning_disability | category | Presence of learning disabilities | - | 0.00% |
| special_education_services | category | Receipt of special education services | - | 0.00% |
| english_language_learner | category | English language learner status | - | 0.00% |

### Technology Access
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| computer_access | category | Access to computer at home | - | 0.09% |
| internet_access | category | Access to internet at home | - | 0.00% |
| digital_literacy_score | float64 | Digital literacy skills rating | score | 0.00% |
| online_learning_experience | category | Experience with online learning | - | 0.00% |
| technology_comfort_level | category | Comfort level with technology | - | 0.00% |

### Target Variables
| Column Name | Data Type | Description | Unit | % Missing |
|-------------|-----------|-------------|------|------------|
| academic_performance_level | category | Academic performance classification (Below Average, Average, Above Average, Excellent) | - | 0.00% |
| college_readiness_score | float64 | College readiness assessment score | score | 0.00% |

## Data Quality Notes

### Missing Values (MNAR - 3%)
- **Missingness Pattern**: Higher missingness in `satisfaction_score` for students with low academic performance
- **Business Logic**: Struggling students may not complete all assessments

### Outliers (0.2%)
- **Score Outliers**: Perfect scores (100%) or extremely low scores (<10%)
- **Age Outliers**: Unrealistic student ages (<13 or >20)
- **Time Outliers**: Negative study hours or impossible attendance rates
- **GPA Outliers**: GPAs above 4.0 or negative values

### Entry Errors (≤30%)
- **Score Errors**: Some students show inconsistent performance across subjects
- **Date Errors**: Future enrollment dates or impossible grade sequences
- **Value Errors**: Negative scores or impossible percentages
- **Demographic Errors**: Inconsistent demographic information

## Target Variable Dependencies

### Academic Performance Level (Classification)
Depends on:
1. **gpa** - Primary predictor (positive correlation)
2. **overall_academic_score** - Higher scores indicate better performance
3. **study_hours_per_week** - More study time improves performance
4. **homework_completion_rate** - Higher completion rates improve performance
5. **class_attendance_rate** - Better attendance improves performance
6. **family_income** - Higher income associated with better performance

### College Readiness Score (Regression)
Depends on:
1. **overall_academic_score** - Primary predictor
2. **gpa** - Higher GPA increases readiness
3. **standardized_test_scores** - Better test scores indicate readiness
4. **study_hours_per_week** - More study time improves readiness
5. **extracurricular_activities** - Well-rounded students have higher readiness
6. **family_support_score** - Family support improves readiness
