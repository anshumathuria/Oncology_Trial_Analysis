# Oncology_Trial_Analysis
# Oncology Clinical Trial Data Pipeline

## Author

Anshu Mathuria

## Project Overview

This project transforms a raw oncology clinical trial dataset into a clean analytical structure and develops a reproducible framework for estimating historical clinical trial success rates.

The work is divided into two stages:

### Part A: Data Ingestion, Profiling and Schema Design

The raw flat-file dataset was audited for quality issues, cleaned, standardized, and transformed into a normalized analytical schema.

Key activities included:

* Data completeness assessment
* Missing value analysis
* Cardinality profiling
* Structural anomaly detection
* Fuzzy matching for categorical inconsistencies
* Controlled vocabulary standardization
* Derived feature engineering
* Analytical schema construction

The final schema follows a star-schema style design consisting of:

#### Fact Table

* FACT_TRIAL

#### Dimension Tables

* DIM_INDICATION
* DIM_DRUG

Additional derived variables include:

* Phase Integer
* Trial Duration (days)
* Combination Therapy Flag
* Enrollment Velocity

Generated outputs:

* cleaned_data_part1.csv
* fact_trial.csv
* dim_indication.csv
* dim_drug.csv

---

## Part B: Success Rate Logic and Cohort Analysis

### Defining Success

The dataset does not contain an explicit success indicator. Therefore, a transparent proxy metric was developed.

#### Success (1)

* COMPLETED trials

#### Failure (0)

* TERMINATED
* SUSPENDED
* WITHDRAWN
* FAILED

#### Excluded Statuses

To avoid right-censoring bias, ongoing or ambiguous trials were excluded:

* RECRUITING
* ACTIVE, NOT RECRUITING
* NOT YET RECRUITING
* ENROLLING BY INVITATION
* Other non-final statuses

Only trials with definitive outcomes were included in the historical cohort.

---

## Cohort Analyses

Three analytical views were generated:

### 1. Indication-Level Success Rates

Comparison of disease-specific success rates against the overall portfolio average.

### 2. Indication × Phase Analysis

Heatmap visualization of success rates across clinical phases and disease indications.

### 3. Temporal Trend Analysis

Assessment of changes in success rates over time.

Small cohorts were suppressed to reduce noise and improve interpretability.

---

## Key Assumptions and Limitations

### Proxy Success Metric

Clinical trial completion is used as a proxy for success. Completion does not necessarily imply:

* Regulatory approval
* Commercial success
* Positive efficacy outcomes

### Right-Censoring

Ongoing trials were excluded because their outcomes are unknown.

### Small Sample Sizes

Rare indications and low-frequency cohorts may produce unstable estimates.

### Data Quality Dependence

Results depend on the accuracy and completeness of the source dataset.

---

## Technologies Used

### Python Libraries

* pandas
* numpy
* matplotlib
* seaborn
* plotly
* missingno
* ast

### Environment

* Jupyter Notebook
* Python 3.x

---

## Repository Structure

├── Part_A.ipynb
├── Part_B.ipynb
├── cleaned_data_part1.csv
├── fact_trial.csv
├── dim_indication.csv
├── dim_drug.csv
└── README.md

---

## Deliverables

* Data quality assessment
* Clean analytical schema
* Success-rate methodology
* Cohort analyses
* Visualizations
* Reproducible Python workflow
