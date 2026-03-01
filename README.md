# Syracuse Unfit Properties Analysis  
### A Reproducible Civic Data & Responsible AI Project

---

## 1. Project Overview

This project analyzes the **City of Syracuse Unfit Properties dataset** to evaluate housing condition reporting, assess data quality, and demonstrate responsible integration of Large Language Models (LLMs) in civic analytics.

The primary goals of this project are:

- Build a fully reproducible data analysis pipeline  
- Assess dataset quality and completeness  
- Generate transparent statistical summaries  
- Integrate LLMs safely for hypothesis generation  
- Validate all AI-generated numeric claims  
- Produce documentation suitable for civic stakeholders  

This project emphasizes **analytical rigor, reproducibility, and accountability**.

---

## 2. Why This Project Matters

Housing quality directly impacts:

- Public health  
- Neighborhood stability  
- Resource allocation  
- Policy enforcement  

Understanding the completeness and limitations of the Unfit Properties dataset enables:

- More informed decision-making  
- Greater transparency  
- Improved data governance  

This project also demonstrates how AI tools can be used responsibly in public sector analytics.

---

## 3. Data Source

**City of Syracuse Open Data Portal**  
Dataset: *Unfit Properties*

- Format: CSV  
- Records analyzed: 264  
- Stored locally in: `data_raw/`  

Raw data is never modified. Cleaned data is saved separately in `data_processed/`.

---

## 4. System Architecture

The project follows a modular pipeline design:

Raw Data → Transform → Analyze → Visualize → LLM Hypothesis → Validate

### Modules

- `config.py` – Path management and directory setup  
- `transform.py` – Raw → clean processing  
- `analyze.py` – Statistical computation  
- `present.py` – Visualization generation  
- `llm.py` – Prompt construction & logging  
- `validate.py` – Numeric hallucination detection  
- `pipeline.py` – End-to-end orchestration  

The entire workflow runs via a single command.

---

## 5. Methodology Summary

### Data Processing
- Raw CSV ingestion  
- Text normalization (whitespace trimming)  
- Date parsing and standardization  
- Data dictionary generation  
- Clean dataset output  

### Statistical Analysis
- Missing value frequency and percentage  
- Row-level completeness distribution  
- Descriptive statistics using pandas  
- Categorical frequency analysis  
- Temporal coverage assessment  

All statistical calculations are deterministic.

---

## 6. LLM Integration Strategy

LLMs are used strictly for **hypothesis generation**, not computation.

### Safeguards Implemented

- Ground-truth statistics computed using pandas  
- LLM responses manually logged  
- Numeric values extracted from responses  
- Compared against computed metrics  
- Unsupported numeric claims flagged  
- Validation report generated  

Output: `llm_validation_report.json`

This ensures AI outputs do not introduce misinformation.

---

## 7. Key Findings

- Total records analyzed: 264  
- The "Vacant" field contains 100% missing values  
- Data completeness varies significantly across records  
- Geographic data is inconsistently populated  

These findings highlight both analytical potential and data limitations.

---

## 8. Reproducibility

This project is fully reproducible.

### Run Full Pipeline

From project root:


This will:
- Generate cleaned dataset
- Compute summaries
- Create visualizations
- Save ground-truth statistics
- Log LLM prompts

### Validate LLM Outputs

### Run Unit Tests

All core functions are tested and verified.

---

## 9. Project Structure
syracuse_unfit_properties/
│
├── data_raw/
├── data_processed/
├── outputs/
│ └── figures/
├── logs/
├── docs/
├── src/
├── tests/
│
├── README.md
├── TECHNICAL.md
├── METHODOLOGY.md
├── PROTOTYPE_SUMMARY.md
├── requirements.txt
├── run_pipeline.py
└── validate_llm.py



---

## 10. Deliverables Included

✔ Modular source code  
✔ Reproducible pipeline  
✔ Data dictionary  
✔ Phase 2 Exploration Report  
✔ LLM validation report  
✔ Unit tests (all passing)  
✔ Technical documentation  
✔ Methodology documentation  
✔ Working prototype summary  
✔ Presentation slides  

---

## 11. Known Limitations

- Dataset reflects reported unfit properties only  
- Geographic completeness may be limited  
- No predictive modeling implemented  
- CLI-based workflow (no interactive dashboard)  
- LLM responses require manual insertion for transparency  

---

## 12. Future Improvements

- Geospatial enrichment (neighborhood overlays)  
- Time-series trend analysis  
- Interactive dashboard deployment  
- Automated CI testing  
- Containerization (Docker)  
- Predictive modeling extension  

---

## 13. Dependencies

- Python 3.8+
- pandas
- numpy
- matplotlib
- pytest

Install via:
pip install -r requirements.txt
---

## 14. Ethical & Responsible AI Considerations

- LLM outputs are clearly labeled as exploratory  
- No automated AI decision-making  
- All numeric claims validated  
- Transparency prioritized over automation  
- Reproducibility maintained at every stage  

---

---

## 15. Conclusion

This project demonstrates how civic data can be analyzed using a structured, reproducible pipeline while responsibly integrating AI tools.  

By combining deterministic computation with validated LLM-assisted insight, the system ensures both analytical rigor and transparency for stakeholders.

The foundation built here can support future policy analysis, geospatial enrichment, and expanded housing research in Syracuse.