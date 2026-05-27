# Exhibit B — Apex Logistics Operations Dashboard

---

**APEX LOGISTICS**
*Fleet Operations — Performance Snapshot*

---

**Prepared by:** Operations Analytics Group
**Reporting Period:** Most Recent Quarter-End
**Data Source:** Transportation Management System — Full Extract
**Total Records:** 450,000 Delivery Records (~3 Years)

---

## Fleet Overview

| Metric | Value |
|---|---|
| Total Delivery Records | 450,000 |
| Data Fields Captured | 22 |
| Source System | Transportation Management System (TMS) |
| Annual Delivery Volume | ~150,000 |
| Fleet Composition | Bike, Van, Truck, Heavy Truck |

---

## Vehicle Type Distribution

| Vehicle Type | Estimated Share | Typical Use Case |
|---|---|---|
| Van | ~35% | Urban/Suburban last-mile |
| Truck | ~30% | Regional freight, multi-stop |
| Bike | ~20% | Dense urban, lightweight |
| Heavy Truck | ~15% | Long-haul, heavy freight |

---

## Route Type Breakdown

| Route Type | Estimated Share | Avg Distance (km) |
|---|---|---|
| Urban | ~40% | ~35 |
| Suburban | ~35% | ~85 |
| Highway | ~25% | ~200 |

---

## Delivery Priority Mix

| Priority Level | Estimated Share |
|---|---|
| Standard | ~50% |
| Express | ~30% |
| Same Day | ~20% |

---

## On-Time Performance by Vehicle Type

| Vehicle Type | On-Time Rate (Approx.) | Minor Delay | Major Delay |
|---|---|---|---|
| Bike | ~60% | ~25% | ~15% |
| Van | ~55% | ~28% | ~17% |
| Truck | ~52% | ~29% | ~19% |
| Heavy Truck | ~48% | ~30% | ~22% |
| **Fleet Average** | **~54%** | **~28%** | **~18%** |

> *On-time rates vary significantly by vehicle type. Heavy Trucks show the highest Major Delay rate, likely reflecting longer distances and weather exposure. Fleet-wide on-time performance has declined from ~62% (earliest records) to below 50% (most recent quarter).*

---

## Weather Condition Impact

| Weather | Share of Deliveries | Estimated On-Time Rate |
|---|---|---|
| Clear | ~50% | ~60% |
| Rain | ~25% | ~52% |
| Fog | ~12.5% | ~48% |
| Snow | ~12.5% | ~42% |

```
On-Time Rate by Weather (Illustrative):

  On-Time %
  60% ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  Clear
  52% ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓      Rain
  48% ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓       Fog
  42% ▓▓▓▓▓▓▓▓▓▓▓▓▓         Snow
  ────────────────────────────
```

> ⚠️ *Snow conditions reduce on-time delivery rates by approximately 18 percentage points relative to Clear weather. The holiday season — when Ridgeline's contract failures occurred — coincides with peak Snow and Fog frequency.*

---

## Driver Experience Distribution

| Experience Range | Estimated Share | Avg On-Time Rate |
|---|---|---|
| 0.5 – 2 years | ~30% | ~47% |
| 2 – 5 years | ~30% | ~53% |
| 5 – 10 years | ~20% | ~58% |
| 10 – 20 years | ~15% | ~63% |
| 20 – 30 years | ~5% | ~68% |
| **Fleet Average** | **~4.5 years** | |

```
Driver Experience Distribution (Illustrative):

  Freq
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓
  ──────────────────────── Years
  0.5    2     5    10   20   30
         ↑median ~4.5
```

> *Approximately 60% of drivers have fewer than 5 years of experience. The on-time performance gap between the least and most experienced cohorts exceeds 20 percentage points — a signal the operations team has flagged for route assignment review.*

---

## Fuel Efficiency by Vehicle Type

| Vehicle Type | Avg Fuel Efficiency (km/L) | Range |
|---|---|---|
| Bike | ~18 | 12 – 20 |
| Van | ~10 | 6 – 15 |
| Truck | ~6 | 4 – 10 |
| Heavy Truck | ~4 | 3 – 7 |
| **Fleet Average** | **~8** | **3 – 20** |

> *Fleet fuel efficiency varies by 5× across vehicle types. Fuel cost as a share of total delivery cost ranges from ~8% for urban bike deliveries to ~35% for long-haul heavy truck routes.*

---

## Delivery Cost Profile

| Statistic | Value |
|---|---|
| Distribution Shape | Log-normal, right-skewed |
| Center (exp of log-mean) | ~$33 |
| Typical Range (IQR) | ~$15 – $85 |
| Full Range | $5 – $8,000+ |

```
Cost Distribution (Illustrative):

  Freq
   ▓
   ▓▓
   ▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓
   ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  ──────────────────────────── Cost ($)
  $5    $33   $85  $500  $8,000+
         ↑center
```

> *The long right tail reflects heavy truck, long-haul, and multi-stop deliveries. Approximately 5% of deliveries account for an estimated 30% of total delivery costs. Current flat-rate pricing does not capture this variation.*

---

## Data Quality Summary

| Issue Category | Records Affected | Share of Dataset |
|---|---|---|
| Missing Values | ~13,500 | ~3.0% |
| Entry Errors | ~22,500 | ~5.0% |
| Outliers | ~900 | ~0.2% |

| Data Quality Metric | Value |
|---|---|
| Total Data Cells | ~9.9 million (450,000 × 22) |
| Total Records with Issues | ~36,900 (some overlap) |
| Fields Most Affected (Missing) | Fuel Efficiency, Driver Rating, Maintenance Score, Traffic Density, Fuel Cost |
| Fields Most Affected (Errors) | Delay Minutes, Num Stops, Actual Duration Hours |
| Fields Most Affected (Outliers) | Distance KM, Load Weight KG, Fuel Cost |
| Missingness Pattern | Non-random — patterns require investigation (MNAR suspected) |

> ⚠️ *Aggregate data quality issues affect approximately 8% of the dataset. However, overlap between categories means the true number of unique affected records may be lower. A field-level audit is recommended before modeling begins. Any client-facing prediction system must document how data quality issues were identified and handled.*

---

## Key Questions for Contract Reinstatement

1. **Prediction Capability:** Can a pre-dispatch model flag at-risk shipments across all three priority tiers with sufficient accuracy to satisfy Ridgeline's requirements?
2. **Delivery Classification:** How are the three delivery outcome classes (On Time / Minor Delay / Major Delay) distributed, and what are the primary drivers of each?
3. **Cost Estimation:** Can dynamic cost predictions replace the flat-rate pricing tables and improve margin accuracy?
4. **Data Integrity:** Are the ~13,500 missing values and ~22,500 entry errors randomly distributed or concentrated in ways that could bias the prediction system?
5. **Driver Assignment:** Does driver experience justify differential route assignment, and what are the equity implications?

---

## Data Resources for Analysis

| Resource | Location |
|---|---|
| Delivery Dataset | `datasets/transportation/synthetic_transportation_20250901.csv` |
| Data Dictionary | `documentation/data_dictionaries/transportation_dictionary.md` |
| Suggested Analysis Tasks | `documentation/suggested_tasks/transportation_tasks.md` |

---

*This dashboard is a fictional business document prepared for case discussion. All statistics are illustrative estimates consistent with the case dataset and should be independently verified by students as part of their exploratory data analysis.*
