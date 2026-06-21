# Oncology Clinical Trial Success Analysis

### Data Engineering & Analytics Pipeline | Interview Assignment

## Project Overview

This project develops a reproducible end-to-end analytics pipeline to evaluate operational success rates in oncology clinical trials.

The source dataset contains 1,000 oncology interventional trials extracted from a clinical trial registry. While rich in information, the raw data was structured for operational data entry rather than analytical reporting. Several columns contained multi-valued fields stored as stringified Python lists, categorical attributes required standardization, and no explicit definition of trial success was available.

The objective of this project was to transform the raw dataset into an analysis-ready schema and generate meaningful insights into clinical trial success patterns across disease indications, clinical phases, and time.

---

## Business Problem

Clinical trial portfolios contain a mixture of completed, terminated, suspended, withdrawn, and actively recruiting studies. Determining which factors are associated with successful trial completion requires:

* Data quality assessment
* Schema normalization
* Feature engineering
* Cohort definition
* Success rate modeling

This project addresses these challenges through a structured data engineering and analytics workflow.

---

## Repository Structure

```text
oncology-clinical-trial-success-analysis/

├── data/
│   └── SampleDateExtract.xlsx
│
├── notebooks/
│   ├── Part_A_Data_Quality_Audit.ipynb
│   └── Part_B_Success_Rate_Analysis.ipynb
│
├── outputs/
│   └── figures/
│
├── schema/
│   ├── fact_trial.xls
│   └── dim_indication.xls
│
├── requirements.txt
└── README.md
```

---

## Part A: Data Quality Audit & Schema Engineering

The first phase focused on understanding the structural integrity of the dataset before any transformations were applied.

### Data Quality Checks

The audit included:

* Missing value assessment
* Completeness and cardinality profiling
* Duplicate trial detection
* Primary key validation
* Date consistency checks
* Chronological integrity validation
* Fuzzy matching for typo detection
* Detection of extreme temporal outliers

### Key Findings

* No duplicate NCT identifiers were detected.
* No missing primary keys were found.
* Date fields passed chronology validation.
* Limited missingness was observed in completion-related fields.
* A small number of completion dates extended beyond expected temporal ranges and were flagged for review.

### Schema Engineering

The raw dataset contained several nested and multi-valued attributes, making direct aggregation difficult.

To improve analytical usability, a normalized analytical schema was designed consisting of:

### FACT_TRIAL

One record per clinical trial containing:

* Trial identifier
* Recruitment status
* Clinical phase
* Trial duration
* Start year
* Combination therapy indicator
* Enrollment velocity

### DIM_INDICATION

A dimension table containing exploded disease indications linked to individual trials.

### Feature Engineering

Several analytical features were derived:

* `phase_integer`
* `trial_duration_days`
* `start_year`
* `is_combination_therapy`
* `enrollment_velocity_per_month`

---

## Part B: Success Rate Cohort Analysis

### Defining Trial Success

The dataset does not contain an explicit success flag.

A defensible operational proxy was constructed using trial recruitment status.

### Success (1)

Trials with status:

```text
COMPLETED
```

### Failure (0)

Trials with status:

```text
TERMINATED
SUSPENDED
WITHDRAWN
FAILED
```

### Excluded (Right-Censored)

Trials with ongoing statuses were excluded from analysis:

```text
RECRUITING
NOT_YET_RECRUITING
ACTIVE_NOT_RECRUITING
ENROLLING_BY_INVITATION
UNKNOWN
```

Including ongoing trials would introduce right-censoring bias because their final outcome is not yet known.

---

## Cohort Summary

| Metric                       | Value |
| ---------------------------- | ----- |
| Total Trials                 | 1,000 |
| Definitive Historical Cohort | 620   |
| Successful Trials            | 453   |
| Failed Trials                | 167   |
| Global Success Rate          | 73.1% |

---

## Analytical Outputs

The project evaluates success rates across three analytical dimensions:

### 1. Success Rate by Indication

Comparison of major oncology indications against the global portfolio average.

### 2. Indication × Phase Heatmap

Visualization of how success rates vary simultaneously across disease indication and clinical development phase.

### 3. Historical Trends

Three-year moving average analysis of success rates over time.

---

## Key Insights

### Portfolio Performance

Among 620 definitive trials, the overall operational completion rate was 73.1%.

### Indication-Level Variation

Success rates varied substantially across oncology indications, suggesting differences in biological complexity, patient recruitment, and competitive therapeutic landscapes.

### Phase-Level Differences

Distinct success patterns emerged across clinical development phases, highlighting critical transition points in drug development.

### Temporal Trends

Historical trends suggest fluctuations in completion rates over time, emphasizing the importance of evaluating performance within a temporal context.

---

## Limitations

This project measures operational success rather than therapeutic success.

A completed clinical trial indicates that the study reached completion according to protocol, but it does not imply that the treatment met efficacy endpoints or received regulatory approval.

A complete therapeutic success analysis would require integration with published trial results and regulatory outcome data.

---

## Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Plotly
* Missingno
* Jupyter Notebook

---

## Author

**Anshu Mathuria**

M.Sc. Biotechnology & Bioinformatics
Institute of Bioinformatics and Applied Biotechnology (IBAB)
