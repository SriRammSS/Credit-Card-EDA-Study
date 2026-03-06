<div align="center">

# 💳 Credit Card EDA — Loan Default Risk Analysis

### End-to-End Exploratory Data Analysis on Financial Risk Data

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Plotly](https://img.shields.io/badge/Plotly-Interactive_Viz-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)](https://plotly.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](LICENSE)

<br/>

> A comprehensive EDA on loan application data to identify applicant profiles associated with payment difficulty — helping a lending institution make informed decisions on loan approval, rejection, and interest rate adjustment.

</div>

---

## Overview

This case study tackles a real-world class imbalance problem in financial risk modelling. The dataset contains **91.9% non-defaulters vs 8.1% defaulters** (imbalance ratio of 11.39:1), making naive accuracy a misleading metric. The analysis uses segmented univariate and bivariate techniques to surface genuine signal from imbalanced data without any model training.

| Dimension | Value |
|-----------|-------|
| Cells | 247 |
| Dataset | Current loan applications + prior application history |
| Target | `TARGET` — 1 = payment difficulty, 0 = no difficulty |
| Class imbalance ratio | **11.39:1** (non-defaulter : defaulter) |
| Key technique | Bivariate segmentation with a custom `biplot()` function |

---

## Analysis Pipeline

```
Raw Data (application_data.csv + previous_application.csv)
        │
        ▼
┌──────────────────────────────────────────────────────────────┐
│  Data Cleaning                                                │
│  • Drop columns >35% null                                    │
│  • Mode/median imputation for remaining nulls                │
│  • Fix DAYS columns (abs() — negative values)                │
│  • 'XNA' gender → 'F', 'XNA' org type → 'Pensioner'        │
│  • Y/N encode → 1/0                                          │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│  Feature Engineering                                          │
│  • AMT_INCOME_TOTAL → 5 quantile bins (VERY_LOW → VERY_HIGH)│
│  • DAYS_BIRTH → age in years → AGE_GROUP (4 bins)           │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│  Imbalance Analysis                                           │
│  • 91.9% non-defaulters, 8.1% defaulters                    │
│  • Ratio: 11.39:1                                            │
└────────────────────────┬─────────────────────────────────────┘
                         │
           ┌─────────────┴─────────────┐
           ▼                           ▼
  Univariate Analysis          Bivariate Analysis
  (Target=0 vs Target=1)       (Categorical × Numerical,
  Gender, age, income,          Categorical × Categorical)
  org type, contract,           Custom biplot() isolates
  family status                 max default % segments
```

---

## Key Findings

| Finding | Detail |
|---------|--------|
| **Class imbalance** | 11.39:1 ratio — any model must use stratified sampling or re-weighting |
| **Gender** | Female applicants apply more; male applicants default at a slightly higher rate |
| **Age** | Middle-age group (35–60) has the highest application and default count |
| **Organisation** | Business Entity Type 3, Self-employed, and Medicine sectors are top applicant sources |
| **Education** | Academic degree holders show tight income/credit distributions — lower default variance |
| **Income vs default** | Defaulters have lower median income and wider spread vs non-defaulters |

---

## Tech Stack

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, feature engineering, groupby analysis |
| `numpy` | Numerical operations, binning |
| `matplotlib` | Static distribution and box plots |
| `seaborn` | Statistical visualisations |
| `plotly` | Interactive charts and subplots |

---

## How to Run

```bash
pip install pandas numpy matplotlib seaborn plotly jupyter
jupyter notebook "Credit EDA Case Study (1).ipynb"
```

> **Note:** Place `application_data.csv` and `previous_application.csv` in the same directory as the notebook before running.
