# Exhibit B — GreenGrid Utilities Building Portfolio Dashboard

**Period: Most Recent 12-Month Baseline | Prepared by: Sustainability Analytics, Office of the Director**

---

## Section 1: Portfolio Overview

### 1.1 Summary Metrics

| Metric | Value |
|--------|-------|
| Total Buildings in Service Territory | 350,000 |
| Data Fields Captured per Building | 21 |
| Building Type Categories | 4 |
| Energy Source Categories | 4 |
| Efficiency Classification Levels | 3 (High, Medium, Low) |

### 1.2 Energy Consumption Profile

| Metric | Value |
|--------|-------|
| **Distribution** | Log-normal |
| **Center** | ~665 kWh (typical mid-range building) |
| **Minimum (Clipped)** | 50 kWh |
| **Maximum (Clipped)** | 50,000 kWh |
| **Right Tail** | ~5% of buildings account for a disproportionate share of total consumption |

The log-normal distribution of energy consumption means that the bulk of buildings cluster in a moderate range, but a long right tail of energy-intensive buildings — primarily large industrial and institutional facilities — has an outsized impact on aggregate consumption. Understanding what drives buildings into that tail is critical for meeting the 30% reduction mandate.

---

## Section 2: Building Type Distribution

### 2.1 Portfolio Composition

| Building Type | Approximate Share | Typical Floor Area | Typical Occupants | Primary Characteristics |
|---------------|-------------------|-------------------|--------------------|------------------------|
| Residential | ~25% | 50–800 m² | 1–15 | Single-family, multi-family, apartments |
| Commercial | ~25% | 200–5,000 m² | 5–100 | Offices, retail, restaurants, services |
| Industrial | ~25% | 500–20,000 m² | 10–200 | Manufacturing, warehousing, processing |
| Institutional | ~25% | 300–10,000 m² | 15–200 | Schools, hospitals, government, religious |

**Key Observation:** The portfolio is approximately evenly distributed across four building types. However, energy consumption, equipment profiles, and retrofit potential vary significantly across types. Industrial and institutional buildings tend to have older equipment, higher peak demands, and lower efficiency scores — making them high-impact retrofit candidates on a per-building basis.

---

## Section 3: Energy Source Mix

### 3.1 Primary Energy Source Distribution

| Energy Source | Approximate Share | Typical Use Case |
|---------------|-------------------|-----------------|
| Natural Gas | ~25% | Heating-dominant buildings, older residential |
| Electricity | ~25% | All-electric buildings, heat pumps, newer commercial |
| Mixed | ~25% | Dual-fuel systems, buildings with multiple load types |
| Renewable | ~25% | Buildings with solar panels and/or renewable energy contracts |

### 3.2 Solar Panel Capacity

| Metric | Value |
|--------|-------|
| Buildings with No Solar Panels | ~40% of portfolio |
| Buildings with Solar Panels | ~60% of portfolio |
| Median Capacity (buildings with panels) | ~4.5 kW |
| Maximum Capacity | 200 kW |
| Distribution | Right-skewed (most installations are small residential) |

**Key Observation:** Approximately 40% of buildings have no installed solar capacity, representing a significant opportunity for the Retrofit Investment Fund. Among buildings with panels, the majority are small residential installations (2–8 kW), while a small number of large commercial and industrial buildings have systems exceeding 50 kW.

---

## Section 4: Efficiency Level Distribution

### 4.1 Current Classification

| Efficiency Level | Class | Description |
|-----------------|-------|-------------|
| High | 0 | Above-average efficiency; modern equipment, good insulation, low waste |
| Medium | 1 | Average efficiency; some improvement opportunities |
| Low | 2 | Below-average efficiency; significant retrofit potential |

**Key Observation:** The distribution across the three classes provides the foundation for retrofit targeting. The ratio of buildings across efficiency tiers — and how that ratio varies by building type, age, and equipment condition — is the central analytical question for fund allocation.

### 4.2 Efficiency Drivers (Preliminary)

| Factor | Relationship to Efficiency | Modifiable? |
|--------|---------------------------|-------------|
| Insulation rating | Higher rating → Higher efficiency | Yes (retrofit) |
| HVAC age | Older systems → Lower efficiency | Yes (replacement) |
| Window efficiency | Higher ratio → Higher efficiency | Yes (replacement) |
| Building age | Older buildings → Lower efficiency | No (structural) |
| Floor area | Larger buildings → Complex relationship | No (structural) |
| Building type | Industrial/Institutional → Lower efficiency | No (structural) |
| Solar capacity | Higher capacity → Higher efficiency | Yes (installation) |
| Smart meter | Smart meter → Modestly higher efficiency | Yes (installation) |

---

## Section 5: Equipment and Systems Profile

### 5.1 HVAC Systems

| Metric | Value |
|--------|-------|
| Median Age | ~6 years |
| Range | 0.5–25 years |
| Typical Service Life | 15–25 years |

### 5.2 Insulation Rating

| Metric | Value |
|--------|-------|
| Center | ~50 (on 15–100 scale) |
| Range | 15–100 |
| Interpretation | Higher = better insulation quality |

### 5.3 Window Efficiency

| Metric | Value |
|--------|-------|
| Center | ~0.50 |
| Range | 0.20–0.95 |
| Interpretation | Thermal efficiency ratio; higher = less heat loss |

### 5.4 Appliance Count

| Metric | Value |
|--------|-------|
| Median | Varies by building type |
| Range | 1–75 (typical) |
| Interpretation | Number of major energy-consuming appliances |

### 5.5 Smart Meter Penetration

| Status | Description |
|--------|-------------|
| Yes | Smart meter installed; real-time consumption monitoring available |
| No | Traditional meter; consumption data available only at billing intervals |

---

## Section 6: Weather Exposure

### 6.1 Climate Conditions Across Service Territory

| Metric | Center | Range |
|--------|--------|-------|
| Outdoor Temperature | ~15°C | −20°C to 45°C |
| Relative Humidity | ~50% | 10%–95% |
| Wind Speed | Varies | Low to high |
| Daylight Hours | Varies by season | ~8–16 hours |

**Key Observation:** The service territory experiences a wide range of climate conditions, from sub-zero winter temperatures to extreme summer heat. Buildings at the tails of the temperature distribution — those exposed to the coldest winters or hottest summers — face the highest heating and cooling loads. Weather sensitivity varies significantly by building type and equipment condition, creating opportunities for climate-targeted retrofit strategies.

---

## Section 7: Data Quality Summary

### 7.1 Missing Values

| Metric | Value |
|--------|-------|
| Records with Missing Values | ~10,500 |
| Overall Missing Rate | ~3% of affected fields |
| Distribution | Not random — concentrated in specific equipment and weather fields |

### 7.2 Known Data Quality Issues

| Issue Type | Estimated Prevalence | Likely Source |
|------------|---------------------|---------------|
| Missing values | ~10,500 records (~3%) | Voluntary audit non-response; incomplete permit records |
| Entry errors | ~17,500 records (~5%) | Self-reported audits with no validation controls |
| Outliers | ~700 records (~0.2%) | Possible aggregation artifacts or data entry errors |

**Context:** GreenGrid's Building Management System was assembled from three sources — utility billing records, municipal building permits, and self-reported energy audits — each with different data capture practices, validation standards, and update frequencies. The data quality issues are not uniform; they reflect the heterogeneous origins of the dataset.

### 7.3 Implications for Targeting

- Equipment fields (insulation rating, HVAC age, window efficiency) sourced from self-reported audits have the highest missingness and error rates. These are precisely the fields most important for identifying retrofit candidates.
- The ~17,500 entry errors in building age, HVAC age, and appliance count are distinguishable from legitimate values by domain knowledge — implausible values exceed physical or operational norms by wide margins.
- Any targeting model must document its cleaning strategy and assess whether performance degrades for subgroups where data quality is poorest — particularly older residential buildings, where audit participation was lowest.

---

## Section 8: Strategic Questions for the Public Utilities Commission

1. **Targeting Efficiency:** What percentage of the 30% reduction target can be achieved by retrofitting the top 10% most inefficient buildings? Is concentration risk acceptable, or should the fund be distributed more broadly?

2. **Building Type Trade-offs:** Industrial and institutional buildings offer the highest per-building energy savings potential. Residential buildings represent the most vulnerable populations. How should the fund balance efficiency impact against equity?

3. **Data Infrastructure:** What investments in building data collection, smart meter deployment, and audit verification are needed to sustain a five-year efficiency program with annual accountability?

4. **Solar Opportunity:** With ~40% of buildings having no solar capacity, should a portion of the Retrofit Investment Fund be directed specifically toward solar installation — or is that better addressed through a separate incentive program?

5. **Weather Resilience:** As climate variability increases, should the targeting model account for future weather exposure, not just current consumption patterns?

---

*All figures in this dashboard are derived from the GreenGrid Utilities Building Management System extract (350,000 building records). This document is prepared for internal planning purposes and case study discussion.*
