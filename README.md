# AIRMAN Aeronautics — Data Science Assessment
## Skynet + TOGA Intelligence Analysis

**Role:** Data Scientist Intern  
**Products:** Skynet (FTO Operations SaaS) + TOGA (Pilot Learning App)  
**Date:** 2026-06-10  

---

## Project Overview

This project analyses simulated data from a Flight Training Organisation (FTO) using AIRMAN's Skynet and TOGA platforms. The goal is to convert aviation training, operations, and finance data into actionable intelligence for FTO leadership, instructors, and the AIRMAN product team.

---

## Folder Structure

```
airman-data-science-assessment/
├── data/
│   ├── sorties.csv              # Flight sortie records
│   ├── aircraft.csv             # Aircraft fleet data
│   ├── cadets.csv               # Cadet enrollment and progress
│   ├── instructors.csv          # Instructor duty and flight hours
│   ├── toga_study.csv           # TOGA app study records
│   ├── payments.csv             # Cadet payment data
│   ├── cleaned_outputs.csv      # Merged, validated master dataset
│   └── risk_scores.csv          # Final cadet risk scores
├── notebooks/
│   └── analysis.ipynb           # Main analysis notebook (all 8 tasks)
├── reports/
│   ├── data_quality_report.md
│   ├── skynet_operations_analysis.md
│   ├── training_progress_analysis.md
│   ├── toga_study_intelligence.md
│   ├── finance_risk_analysis.md
│   ├── executive_insights.md
│   └── methodology.md
├── charts/
│   ├── aircraft_utilization.png
│   ├── cancellation_reasons.png
│   ├── cadet_progress.png
│   ├── study_readiness.png
│   ├── payment_risk.png
│   ├── cadet_risk_scores.png
│   └── flight_vs_study_progress.png
└── README.md
```

---

## Tools and Libraries Used

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, transformation |
| `numpy` | Numerical operations and normalizations |
| `matplotlib` | Chart generation |
| `seaborn` | Styling and heatmaps |
| `json` | Notebook serialization |

Python version: 3.10+

---

## Setup Instructions

```bash
# 1. Clone or extract the project
cd airman-data-science-assessment

# 2. Install dependencies
pip install pandas numpy matplotlib seaborn jupyter

# 3. Launch Jupyter
jupyter notebook notebooks/analysis.ipynb
```

Or open directly in **Google Colab** by uploading the notebook and the `data/` folder.

---

## How to Run the Notebook

1. Open `notebooks/analysis.ipynb`
2. Run cells sequentially from top to bottom
3. All charts auto-save to `charts/`
4. All reports are pre-generated in `reports/`
5. Risk scores are saved to `data/risk_scores.csv`

---

## Data Assumptions

1. Analysis reference date is **2026-06-10**
2. Actual sortie duration is calculated from `actual_end - actual_start`
3. Delay is calculated from `actual_start - scheduled_start`
4. Study inactivity ceiling: 60 days (for normalization)
5. Average delay ceiling: 40 minutes (for normalization)
6. Cancellation count ceiling: 3 (for normalization)
7. PPL and CPL cadets are evaluated on the same risk scale (acknowledged limitation)

---

## Metrics Calculated

| Metric | Formula |
|--------|---------|
| Aircraft Utilization | `actual_flown_hours / total_available_hours × 100` |
| Flight/Duty Ratio | `total_flight_hours / total_duty_hours × 100` |
| Completion Rate | `completed_sorties / total_sorties × 100` |
| Cadet Progress | `total_flown_hours / total_required_hours × 100` |
| Flying Rate | `total_flown_hours / (days_enrolled / 7)` |
| Subject Readiness | `0.4×study_progress + 0.4×quiz_score + 0.2×practice_score` |
| Payment Collection | `paid_amount / invoiced_amount × 100` |

---

## Risk Score Explanation

The Cadet Risk Score (0–100, higher = more risk) is a weighted composite:

| Component | Weight | Why |
|-----------|--------|-----|
| Low flight progress | 25% | Core outcome metric |
| Low study progress | 20% | Ground knowledge is flight safety |
| Low quiz score | 15% | Exam readiness predictor |
| Study inactivity | 15% | Predicts disengagement and dropout |
| Payment outstanding | 15% | Training suspension risk |
| Frequent cancellations | 5% | Scheduling/aircraft reliability signal |
| High average delay | 5% | Operational efficiency signal |

**Thresholds:** 0–39 = Low | 40–69 = Medium | 70–100 = High

---

## Key Outputs

| Cadet | Flight Progress | Risk Score | Risk Level |
|-------|----------------|-----------|-----------|
| Arjun Menon | 63.3% | ~38 | Low-Medium |
| Meera Iyer | 37.0% | ~72 | High |
| Rahul Nair | 26.7% | ~82 | High |

---

## Known Limitations

1. Dataset is small (3 cadets, 15 sorties) — scores are directional, not statistically validated
2. No simulator hours included — understates CPL training progress
3. PPL and CPL cadets evaluated on same scale — course-normalized comparison would be more fair
4. No seasonal weather baseline — cannot distinguish normal weather delays from systemic issues
5. Payment plan type unknown — may penalize cadets on legitimate installment plans

---

## What I Would Improve With More Time

1. Add course-specific progress benchmarking (PPL vs CPL normalization)
2. Build a time-series sortie frequency trend per cadet
3. Add weather API integration for contextualizing weather cancellations
4. Create an interactive Plotly/Dash dashboard for Skynet integration
5. Backtest the risk model against historical FTO outcome data
6. Add DGCA syllabus stage tracking (Stage 1 / Stage 2 / Pre-CPL) to progress analysis

---

## AI Usage Disclosure

1. **Did you use AI tools?** Claude (Anthropic) was used to help structure the project, generate report text, and review methodology framing.

2. **What tasks did AI help with?** Report narrative writing, formula documentation, and Jupyter notebook cell organization.

3. **Which parts did you personally verify?** All formulas (risk score, utilization, dispatch reliability, payment calculations) were independently verified by manual cross-checking against the raw CSV data.

4. **Which AI suggestions did you reject or modify?** Initial suggestion to use a ML classifier (Random Forest) was rejected in favor of an explainable weighted formula as required by the assessment.

5. **Which part are you least confident about?** The inactivity ceiling of 60 days is an assumption — real FTO data would calibrate this threshold more precisely.

6. **Explain one formula in your own words:** The Subject Readiness Score (0.4×study_progress + 0.4×quiz_score + 0.2×practice_score) gives equal weight to chapter completion and quiz performance because both matter equally for exam readiness. Practice tests get lower weight because they are a supplement, not a primary indicator — a cadet who completes all chapters and scores well on quizzes is ready even with few practice tests.
