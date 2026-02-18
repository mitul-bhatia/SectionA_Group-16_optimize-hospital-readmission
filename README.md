# Hospital Readmission Analysis
**Sector:** Healthcare Analytics | **Course:** Data & Visual Analytics Capstone Project | **Group:** Section A - Group 16

---
<img width="2752" height="1536" alt="image" src="https://github.com/user-attachments/assets/56ea3d2e-4d21-4882-b711-3e0ee9231f25" />


## Executive Summary

Hospital readmissions within 30 days are a critical performance and cost indicator in healthcare systems. This project analyzes patient data from **130 US Hospitals (1999–2008)** across multiple conditions (Circulatory, Diabetes, Respiratory, and Others) to identify key drivers of 30-day readmission and provide actionable recommendations for reducing avoidable readmissions.

### Key Metrics at a Glance

| Metric | Value |
|--------|-------|
| Total Patients Analyzed | 14,116 |
| 30-Day Readmission Rate | 13.20% |
| Total Revenue Leakage | $20,493,000 |
| A1C Untested Rate | 83.10% |
| High-Risk Patients | 7.2% (1,013 patients) |

---

## Problem Statement

To identify key demographic, clinical, and administrative factors that influence 30-day hospital readmission across chronic conditions—enabling hospitals to reduce costs and improve patient outcomes.

---

## Dataset

**Source:** [UCI Machine Learning Repository - 130-US Hospitals](https://archive.ics.uci.edu/ml/datasets/Diabetes+130-US+hospitals+for+years+1999-2008)

| Aspect | Details |
|--------|---------|
| Original Size | ~101,766 rows, 50+ columns |
| Final Dataset | 14,116 rows (single encounter per patient) |
| Period | 1999–2008 |
| Processing | Google Sheets |

### Key Limitations
- Historical data (1999–2008)
- No BMI data (weight dropped due to 97% missing)
- No socioeconomic variables

---

## Data Cleaning & Transformation

All data cleaning performed in Google Sheets:

- **Single Encounter Rule:** Retained only first encounter per patient
- **Missing Values:** Race "?" → Caucasian (mode); Gender invalid rows deleted
- **Dropped Columns:** Weight (97% missing), Payer code (40% missing), 24 medication columns
- **Feature Engineering:**
  - `Primary_Condition` (ICD-9 grouping: Diabetes, Circulatory, Respiratory, Other)
  - `A1C_None`, `A1C_High`, `max_glu_high` (binary flags)
  - `High_Risk_Flag` (Readmitted + A1C High)
  - `Total Cost` estimation ($11,000 per readmission)

---

## Key Insights

1. **Emergency admissions** account for 56% of patients with 14.1% readmission rate and $12.3M cost
2. **83.1% A1C testing gap** — majority of patients had no A1C test recorded
3. **94.9% glucose test gap** — almost no max glucose testing
4. **Age 80-90** shows highest readmission rate (14.7%)
5. **Longer hospital stays** (>4.5 days) correlate with higher readmission risk
6. **Medication changes** increase readmission risk (14.3% vs 12.2% for stable)
7. **Circulatory conditions** have the highest readmission share

---

## Dashboard

Interactive dashboard built in Google Sheets with filters for Age, Primary Condition, and Medication Status.

### Dashboard Preview

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b8c742f3-6938-4301-80d1-b91c9d6a8ae6" />


*Filters: Age Group (0-100) | Primary Condition | Medication Status*

**Dashboard Components:**
- Readmission by Admission Type (Pie Chart)
- Cost vs Risk by Readmission Rate (Bar + Line)
- Readmission Rate by Condition (Horizontal Bar)
- Readmission Rate by Age (Line Chart)
- Time in Hospital by Primary Condition (Bar)
- Discharge Location Distribution (Pie Chart)

---

## Recommendations

| # | Recommendation | Impact |
|---|----------------|--------|
| 1 | **Standardize A1C Testing** at discharge | Addresses 83% testing gap |
| 2 | **Emergency Discharge Checklist** | Targets highest cost pathway |
| 3 | **Auto-Flag Long Stay Patients** (>4.5 days) | Early intervention trigger |
| 4 | **High-Risk Follow-Up Program** | Target 1,013 flagged patients |

**Estimated Savings:** $1–2M annually (with 5% readmission reduction)

---

## Project Structure

```
├── README.md
├── 1.Raw Dataset/
│   └── dataset.csv              # Original UCI dataset
├── 2.Cleaned DataSet/
│   ├── cleaned.csv              # Processed dataset (14,116 rows)
│   └── cleaned.md               # Data dictionary
├── 3.PivotTable&Calcualtions/
│   └── Pivot_Table_&_Analytics.csv
└── 4.Dashboard/
    └── Dashboard.csv            # Dashboard data source
```

---

## Team Contribution Matrix

| Team Member | Dataset & Sourcing | Cleaning | KPI & Analysis | Dashboard | Report Writing | PPT | Role |
|-------------|:------------------:|:--------:|:--------------:|:---------:|:--------------:|:---:|------|
| **Mitul Bhatia** | ✔ | ✔ | ✔ | ✔ | ✔ |  ✔ | Project Lead |
| **Divya Singh** | ✔ | ✔ | ✔ | | ✔ | | Data Lead |
| **Dhruv Ramani** | ✔ | ✔ | ✔ | ✔ | | | Analysis Lead |
| **Aaryan Gera** | ✔ | | ✔ | ✔ | | | Dashboard Lead |
| **Anushka Tyagi** | | ✔ | ✔ | | ✔ | ✔ | PPT & Quality Lead |
| **Daniel Tayal** | | ✔ | ✔ | ✔ | | | Strategy Lead |

---

## Future Scope

- Predictive ML model for readmission risk
- Logistic regression risk scoring
- External validation on modern data (post-2020)
- Integration with EMR systems

---

## Conclusion

This project successfully cleaned and structured complex healthcare data, identified readmission risk drivers, quantified financial impact (~$20.5M), and developed actionable dashboard insights. The framework supports hospital administrators in prioritizing high-risk patients and reducing avoidable readmissions.

---

*Declaration: We confirm that the above contribution details are accurate and verifiable.*

