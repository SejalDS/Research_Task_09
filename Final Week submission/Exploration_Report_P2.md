# Phase 2: Exploration Report
## Syracuse Unfit Properties Dataset

---

# 1. Introduction

This report presents an exploratory analysis of the City of Syracuse Unfit Properties dataset. The objective is to assess data quality, identify patterns, and surface insights that may inform civic decision-making.

---

# 2. Data Quality Assessment

## 2.1 Missing Values

Key findings:

- Total records: 264
- The "Vacant" column contains 100% missing values.
- Several fields exhibit partial missingness.
- Row-level completeness varies across records.

Impact:
High missingness limits the reliability of certain variables for analysis.

---

## 2.2 Inconsistencies

- Minor whitespace inconsistencies observed in text fields.
- Date parsing required normalization.
- No major encoding issues detected.

---

## 2.3 Temporal Coverage

- Date fields successfully parsed.
- No obvious extreme outliers detected.
- Temporal gaps require further investigation if used for trend analysis.

---

## 2.4 Geographic Coverage

- Some geographic fields incomplete.
- Neighborhood-level analysis limited without external boundary data.

---

# 3. Summary Statistics

Descriptive statistics generated using pandas:

- Missingness percentages
- Numeric summaries (where applicable)
- Categorical frequency counts
- Row completeness distribution

All statistics saved to outputs folder.

---

# 4. Visualizations

Generated figures include:

1. Top 10 missing columns (bar chart)
2. Row completeness histogram
3. Top categorical values
4. Additional distribution plots

Each visualization was generated using matplotlib and saved to `outputs/figures/`.

---

# 5. Key Findings

1. The "Vacant" field is entirely missing (100% missing).
2. Data completeness varies significantly across records.
3. Certain categorical variables dominate reporting patterns.
4. Geographic information is inconsistently populated.

---

# 6. LLM-Assisted Hypotheses

LLMs were used to generate exploratory hypotheses based on computed statistics.

Hypotheses were validated against ground-truth metrics to prevent unsupported claims.

No hallucinated numeric values were detected.

---

# 7. Limitations

- Dataset reflects only reported unfit properties.
- Missing fields reduce analytical scope.
- No predictive modeling performed.
- LLM outputs are exploratory.

---

# 8. Conclusion

The dataset provides a structured foundation for analyzing housing condition reporting in Syracuse. While data quality limitations exist, the reproducible pipeline ensures transparency and accountability in analysis.

Future work could integrate geographic overlays and trend analysis.