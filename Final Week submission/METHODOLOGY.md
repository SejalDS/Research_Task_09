# Methodology

## 1. Overview

This project analyzes the City of Syracuse Unfit Properties dataset using a structured, reproducible analytical pipeline. The methodology emphasizes deterministic computation, transparency, and responsible integration of Large Language Models (LLMs).

The workflow follows:

Raw Data → Cleaning → Analysis → Visualization → LLM Hypothesis → Validation

---

## 2. Data Processing Steps

### 2.1 Data Acquisition
- Dataset downloaded in CSV format from the City of Syracuse Open Data Portal.
- Stored locally in `data_raw/`.
- Raw data is never modified.

### 2.2 Data Cleaning and Transformation
The following preprocessing steps were applied:

- Text normalization (whitespace trimming)
- Standardization of string columns
- Parsing date-like columns into datetime format
- Creation of a structured data dictionary template
- Clean dataset saved to `data_processed/`

No imputation or recoding was performed to avoid introducing assumptions.

---

## 3. Analytical Approach

All statistical analysis was conducted using pandas.

### 3.1 Missing Value Assessment
- Frequency of missing values per column
- Percentage missing per column
- Row-level completeness distribution

### 3.2 Descriptive Statistics
- Numeric summary statistics (count, mean, min, max, etc.)
- Categorical frequency distributions
- Text consistency checks

### 3.3 Temporal Coverage
- Date parsing validation
- Assessment of date completeness
- Identification of potential gaps in coverage

All outputs were saved as deterministic CSV and JSON files.

---

## 4. LLM Integration Strategy

LLMs were used only for hypothesis generation and narrative exploration.

### 4.1 LLM Workflow

1. Compute ground-truth statistics using pandas
2. Generate structured prompt using those statistics
3. Manually insert LLM response into log file
4. Validate numeric claims against computed statistics

LLMs were never used to compute statistics.

---

## 5. Validation Strategy

To prevent hallucination:

- Numeric values are extracted from the LLM response
- Compared against ground-truth metrics
- Unsupported numbers are flagged
- A validation report is generated (`llm_validation_report.json`)

This ensures analytical integrity.

---

## 6. Limitations

- Dataset reflects reported unfit properties only
- Missing geographic fields limit spatial analysis
- No predictive modeling implemented
- LLM outputs are exploratory and not authoritative

---

## 7. Ethical Considerations

- All numeric claims are validated
- Hypotheses are clearly labeled as unconfirmed
- Transparency prioritized over automation
- No external API calls used

---

## 8. Reproducibility

- Deterministic pipeline execution
- No randomness introduced
- All intermediate outputs persisted to disk
- Single-command execution via `run_pipeline.py`

This ensures that any stakeholder can reproduce the analysis.