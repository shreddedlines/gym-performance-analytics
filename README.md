# Workout Performance Analytics & Recovery Modeling System

> End-to-end data analytics and data science project — from raw WhatsApp workout logs to an interactive Power BI dashboard with statistical inference and machine learning.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Core Research Questions](#core-research-questions)
- [Data Sources](#data-sources)
- [Pipeline Architecture](#pipeline-architecture)
- [Part 1 — Statistical Inference](#part-1--statistical-inference)
- [Part 2 — Recovery Risk Classification](#part-2--recovery-risk-classification)
- [Power BI Dashboard](#power-bi-dashboard)
- [Key Insights](#key-insights)
- [Tools & Technologies](#tools--technologies)
- [Limitations & Future Work](#limitations--future-work)

---

## Project Overview

This project transforms raw, unstructured WhatsApp workout logs into a fully analytical system. It covers the entire data science lifecycle: data extraction, feature engineering, statistical hypothesis testing, machine learning modeling, and interactive dashboarding.

The goal is to go beyond surface-level visualization — applying statistical reasoning and ML to understand strength adaptation patterns and recovery-related performance fluctuations.

---

## Repository Structure

```
workout-performance-analytics/
│
├── notebooks/
│   ├── 01_extract_whatsapp_logs.ipynb       # Parse raw chat exports into structured data
│   ├── 02_feature_engineering.ipynb         # Build longitudinal features, lag variables
│   ├── 03_weekly_aggregation.ipynb          # Aggregate metrics by week
│   └── 04_analysis.ipynb                    # Hypothesis testing + ML modeling
│
├── data/
│   ├── raw/
│   │   ├── previous_training_log.xlsx        # Historical structured training records
│   │   └── bodyweight_log.xlsx               # Daily bodyweight records
│   ├── processed/
│   │   ├── workout_raw_extracted.csv         # Output of extraction notebook
│   │   ├── feature_engineered_dataset.csv    # Output of feature engineering
│   │   └── workout_weekly_analysis.csv       # Final weekly aggregated dataset
│
├── sql/
│   └── ...                                   # Analytical SQL queries
│
├── dashboard/
│   ├── workout_dashboard.pbix                # Power BI dashboard file
│   └── dashboard_overview.png
└── README.md
```

> **Note:** Raw WhatsApp chat exports are excluded from this repository for privacy. Only cleaned analytical datasets are included.

---

## Core Research Questions

1. Does caloric phase (Bulk vs Cut) significantly impact weekly strength adaptation?
2. Can next-week performance drops be predicted using training metrics alone?
3. How is training volume distributed across muscle groups?
4. How does relative strength behave compared to bodyweight trends?

---

## Data Sources

| Source | Description |
|---|---|
| WhatsApp Workout Logs | Unstructured text entries, inconsistent formatting, multiple gyms and phases |
| Historical Training Records | Structured logs merged for continuity across training periods |
| Bodyweight Tracking | Daily records aggregated into weekly averages |

---

## Pipeline Architecture

All data engineering was done in Python (Pandas, NumPy):

1. **Extraction** — Parse unstructured WhatsApp logs into tabular format
2. **Standardization** — Normalize exercise names, map to muscle groups, convert weight units
3. **Volume Calculation** — Compute training volume as `weight × reps`
4. **Strength Estimation** — Apply the Epley 1RM formula
5. **Weekly Aggregation** — Aggregate all metrics at the weekly level
6. **Feature Engineering** — Create lag-based longitudinal features
7. **Leakage Prevention** — Apply time-aware train-test splits throughout

---

## Part 1 — Statistical Inference

**Hypothesis:**

- H₀: Bulk and Cut phases produce equal weekly strength adaptation
- H₁: There is a significant difference in weekly strength change between phases

**Methodology:** Week-over-week strength delta → Welch's t-test → Cohen's d effect size

**Results:**

| Metric | Value |
|---|---|
| P-value | 0.36 |
| Cohen's d | 0.11 |

**Interpretation:** No statistically significant difference was found. Strength adaptation is not driven solely by caloric phase — weekly fluctuations contain substantial noise, and recovery-related variables likely play a larger role.

---

## Part 2 — Recovery Risk Classification

**Objective:** Predict whether next week's strength will decline.

**Target:** `1` = strength drop next week, `0` = no drop

**Features used:**
- Previous week strength (lag)
- Previous week training volume
- Previous week strength trend
- Phase (Bulk/Cut)
- Muscle group

**Models & Results:**

| Model | ROC-AUC |
|---|---|
| Logistic Regression | 0.47 |
| Random Forest | 0.58 |

**Interpretation:** Weak predictive performance indicates that short-term performance drops are not strongly predictable from training metrics alone. Key recovery variables (sleep, stress, nutrition detail) are absent from the dataset. This negative result is itself a meaningful finding about the limits of observable training data.

---

## Power BI Dashboard

An interactive KPI-driven dashboard was built as the final presentation layer.

**Features:**
- Dynamic metric selection (Average / Maximum / Minimum)
- Year-based filtering
- Strength and relative strength trends
- Bodyweight vs. relative strength comparison
- Bulk vs. Cut phase distribution
- Training volume by muscle group
- Recovery status tracking

The dashboard enables multi-perspective analysis while surfacing the nuance that simple averages can obscure.

---

## Key Insights

- Caloric phase alone does not significantly impact weekly strength adaptation
- Strength progression contains substantial short-term variance
- Predicting single-week performance drops with training-only features is unreliable
- Recovery modeling likely requires additional physiological data (sleep, HRV, nutrition)

---

## Tools & Technologies

| Category | Tools |
|---|---|
| Data Engineering | Python, Pandas, NumPy |
| Statistical Testing | SciPy |
| Machine Learning | Scikit-learn |
| Visualization | Matplotlib, Seaborn |
| Analytical Querying | SQL Server |
| Dashboard | Power BI |
| Version Control | Git / GitHub |

---

## Limitations & Future Work

**Current limitations:**
- Limited dataset size
- No direct recovery metrics (sleep, HRV, stress, nutrition)
- Weekly aggregation may mask intra-week patterns
- High variance in strength adaptation

**Future directions:**
- Integrate wearable data (e.g., Garmin, Whoop, Apple Watch)
- Add detailed nutrition tracking
- Explore daily-level modeling to capture finer patterns

---

## Author

**Kshitish** — Data Science Undergraduate

