# TECHNICAL.md  
## Syracuse Unfit Properties — Architecture & Development Documentation (Phase 3)

---

## 1. Overview

This document describes the technical architecture, design decisions, and implementation details for the **Syracuse Unfit Properties** civic data project. The project analyzes publicly available housing data from the City of Syracuse Open Data Portal and implements a reproducible, validated, and extensible data analysis pipeline with Large Language Model (LLM) augmentation.

This document satisfies the **Week 6 Architecture Review** requirement for Phase 3.

---

## 2. System Architecture

### 2.1 High-Level Data Flow

The system is designed as a **modular, file-based pipeline** with clear separation between data acquisition, transformation, analysis, presentation, and validation.

```mermaid
flowchart LR
    A[Raw CSV<br/>data_raw/Unfit_Properties.csv]
    B[Transform<br/>text cleanup & date parsing]
    C[Clean Dataset<br/>data_processed/Unfit_Properties_clean.csv]
    D[Analysis Layer<br/>statistics & summaries]
    E[Outputs<br/>CSV + JSON]
    F[Visualizations<br/>PNG figures]
    G[LLM Prompt Generation]
    H[LLM Response Log]
    I[Validation<br/>Ground Truth Check]

    A --> B --> C
    C --> D --> E
    C --> F
    E --> G --> H --> I

## 4. Module Responsibilities

### 4.1 `config.py`

- Centralizes all project paths  
- Ensures required directories exist  
- Prevents hard-coded file paths throughout the codebase  

---

### 4.2 `transform.py`

Responsible for **raw → clean** transformation:

- Trims whitespace from text fields  
- Parses date-like columns into normalized datetime fields  
- Generates a data dictionary template based on observed schema  

No imputation or recoding is performed at this stage to avoid premature assumptions.

---

### 4.3 `analyze.py`

Performs analytical computation:

- Missing value frequency and percentage  
- Text inconsistency detection  
- Temporal coverage assessment  
- Numeric and full descriptive summaries  
- Generation of ground-truth metrics used for validation  

Outputs are saved as deterministic CSV and JSON files.

---

### 4.4 `present.py`

Handles presentation-layer outputs:

- Missingness bar chart  
- Row completeness histogram  
- Top-category frequency plots  

All visualizations are generated using **matplotlib** to ensure reproducibility.

---

### 4.5 `llm.py`

Implements LLM prompt engineering and logging:

- Builds structured prompts using ground-truth statistics  
- Logs prompts and responses to JSON for traceability  
- Supports iterative prompt refinement without overwriting history  

No automated API calls are made; responses are manually inserted to maintain transparency.

---

### 4.6 `validate.py`

Implements LLM output validation:

- Extracts numeric values from LLM responses  
- Compares them against ground-truth statistics  
- Flags hallucinated or unsupported numeric claims  
- Generates a machine-readable validation report  

This ensures that LLM assistance does not introduce unverified claims.

---

### 4.7 `pipeline.py`

Coordinates the end-to-end pipeline:

- Loads raw data  
- Executes transformation, analysis, and visualization steps  
- Generates all outputs and logs  
- Returns a summary dictionary for inspection  

This module enables full reproducibility via a single command.

---

## 5. Reproducibility & Execution

### 5.1 Running the Pipeline

From the project root:

```bash
python run_pipeline.py

### 5.2 Determinism

- Given the same raw dataset, the pipeline produces identical outputs  
- No randomness is introduced  
- All intermediate and final artifacts are persisted to disk  

---

## 6. LLM Integration Strategy

LLMs are used **only for hypothesis generation and narrative support**, not for numerical computation.

### Safeguards

- Ground-truth statistics are computed using Pandas  
- LLM outputs are validated against those statistics  
- Hypotheses are explicitly labeled as unconfirmed  
- A strict numeric hallucination check is enforced  

This approach balances exploratory insight with analytical rigor.

---

## 7. Quality Assurance

### 7.1 Validation Artifacts

- `ground_truth_findings.json`  
- `llm_validation_report.json`  

---

### 7.2 Error Handling

- Explicit checks for missing raw files  
- Graceful handling of empty or non-parseable columns  
- Conservative validation rules to prevent overclaiming  

---

## 8. Dependencies & Environment

### Core Dependencies

- Python 3.8+  
- pandas  
- numpy  
- matplotlib  

### Platform Considerations

- Developed and tested on Windows  
- Uses file-based execution to avoid environment-specific services  
- No external APIs required  

---

## 9. Current Status & Blockers

### Completed

- End-to-end working prototype  
- Reproducible analysis pipeline  
- LLM prompt logging and validation  
- Visual outputs and summaries  

### Known Limitations

- No interactive user interface (by design)  
- Geographic analysis limited by coordinate completeness  
- LLM responses require manual insertion for transparency  

No active blockers at this stage.

---

## 10. Future Extensions

Potential enhancements include:

- Integration of neighborhood boundary datasets  
- Interactive dashboards (e.g., Tableau or web-based)  
- Time-series modeling of enforcement activity  
- Automated CI testing and containerization  

---

## 11. Conclusion

This architecture prioritizes **clarity, reproducibility, and accountability**.  
The system is intentionally modular, allowing each component to be independently inspected, tested, and extended.  
The combination of deterministic analysis with validated LLM assistance ensures both technical rigor and interpretability for civic stakeholders.
