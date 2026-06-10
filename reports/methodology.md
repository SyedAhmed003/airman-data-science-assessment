# Methodology Document — Explainable Cadet Risk Score
**Project:** AIRMAN Aeronautics – Skynet + TOGA Assessment  
**Date:** 2026-06-10  

---

## 1. Risk Score Formula

The Cadet Risk Score is a weighted composite score ranging from **0 (no risk) to 100 (critical risk)**.

```
Risk Score = 
  (1 - flight_progress%) × 25     [Flight Progress Risk]
+ (1 - avg_study_progress%) × 20  [Study Progress Risk]
+ (1 - avg_quiz_score%) × 15      [Knowledge Readiness Risk]
+ min(days_inactive / 60, 1) × 15 [Study Inactivity Risk]
+ (1 - payment_pct%) × 15         [Financial Risk]
+ min(cancel_count / 3, 1) × 5    [Disruption Risk]
+ min(avg_delay / 40, 1) × 5      [Operational Delay Risk]
```

**Total: 100 points**

**Risk Levels:**
- 0–39 = Low
- 40–69 = Medium
- 70–100 = High

---

## 2. Feature Justification

| Feature | Weight | Justification |
|---------|--------|--------------|
| Flight Progress | 25% | Primary measure of training advancement. Directly determines graduation timeline. |
| Study Progress | 20% | TOGA study underpins theoretical knowledge required for safe flying and exams. |
| Quiz Score | 15% | Low quiz scores indicate weak ground knowledge — a flight safety concern. |
| Study Inactivity | 15% | Extended inactivity (>30 days) predicts disengagement and exam failure risk. |
| Payment Status | 15% | Unpaid dues often lead to training suspension, creating compounding delays. |
| Cancellation Frequency | 5% | Repeated cancellations slow progress and signal scheduling or aircraft reliability issues. |
| Avg Delay | 5% | Chronic delays indicate operational inefficiency at the cadet or instructor level. |

---

## 3. Assumptions Made

1. A 60-day inactivity window is used as the normalization ceiling for study inactivity risk.
2. A 40-minute average delay is used as the ceiling for delay risk normalization.
3. 3 cancellations is used as the ceiling for cancellation risk normalization.
4. Equal weight is given to all TOGA subjects — in practice, subjects closer to exam date may deserve higher weight.
5. The model treats all cadets (PPL and CPL) on the same scale — a limitation since CPL cadets inherently have more hours remaining.

---

## 4. Data Quality Issues That Could Mislead the Model

1. **Small dataset (3 cadets, 15 sorties):** Risk scores are directionally correct but cannot be validated statistically.
2. **Missing TOGA subjects:** C003 has only Navigation data — other subjects may exist but weren't recorded. This artificially inflates their study risk.
3. **No medical/personal context:** A cadet with a temporary medical hold may appear "at risk" for flight progress when it's entirely justified.
4. **Payment timing context:** A payment made 60 days ago may be on a quarterly plan — without installment plan data, we penalize legitimate payers.

---

## 5. What Should NOT Be Automated Yet

1. **Training suspension decisions** — these must involve human judgment (CFI + management).
2. **Instructor reassignment** — involves HR, qualifications, and interpersonal dynamics.
3. **Medical fitness assessments** — strictly regulated by DGCA.
4. **Exam readiness sign-off** — must remain with certified instructors.
5. **Individual cadet counseling** — emotionally sensitive; algorithm scores should never be shown directly to cadets without professional interpretation.

---

## 6. Model Validation with Real FTO Data

1. **Backtest:** Apply the model to historical cadet cohorts and check if high-risk cadets actually dropped out, failed exams, or required extensions.
2. **Expert Calibration:** Have CFIs and FTO managers review scores for 20–30 real cadets and adjust weights based on their disagreements.
3. **Outcome Tracking:** Tag cadets with their final outcome (passed/failed/deferred) and correlate with risk scores using AUC-ROC or F1 metrics.
4. **A/B Testing:** For cadets flagged as medium risk, apply intervention for half and track if intervention group performs better.

---

## 7. Preventing Unfair Ranking of Cadets

1. **Contextualize by course type:** PPL cadets should not be compared directly to CPL cadets. Use course-normalized progress.
2. **Temporal fairness:** A recently enrolled cadet will naturally have lower hours — enrollment date context must adjust the progress expectation.
3. **Flag, don't rank publicly:** Risk scores should be visible to instructors and management — never as a public leaderboard or competitive rank.
4. **Medical/personal flags:** Add override flags for cadets with justified absences (medical, personal emergency) that pause the inactivity timer.
5. **Regular recalibration:** Weights should be reviewed every semester with real outcome data to prevent systemic bias.

---

## 8. How AIRMAN Should Display This Without Demotivating Students

1. **Show cadets a "Health Dashboard"** with positive framing: "Your study momentum," "Your flight readiness," "Areas to strengthen" — not a raw risk score.
2. **Actionable nudges, not alarms:** Instead of "Risk Level: High," show "Complete 3 more Meteorology chapters to boost your readiness score."
3. **Progress-focused language:** TOGA should say "You're 67% ready for your Navigation exam — here's what to focus on" rather than "You scored 42/100."
4. **Instructor view vs Cadet view:** Instructors see the full risk score; cadets see a positive, improvement-oriented version.

---

## 9. Additional Data That Would Improve the Model

1. **Simulator hours** — ground simulator is part of CPL training; ignoring it understates theoretical progress.
2. **Weather patterns by base** — to separate weather cancellations (uncontrollable) from avoidable cancellations.
3. **Previous exam scores** — theoretical examination results are strong predictors of flight test performance.
4. **Instructor feedback scores** — post-sortie debrief ratings would add a qualitative dimension.
5. **Medical certificate status** — a DGCA Class 2 (PPL) or Class 1 (CPL) lapse immediately halts training.
6. **Cadet age and background** — prior aviation experience, ab-initio students, etc. set different baselines.

---

## 10. How This Analysis Helps Skynet and TOGA

**Skynet:**
- FTO operations dashboard can show real-time utilization, cancellation trends, and financial status in one view.
- Automated alerts for aircraft with defect counts crossing thresholds (e.g., >7 defects → maintenance review trigger).
- Instructor workload balancing module — reassign sorties when one instructor approaches duty-hour limits.

**TOGA:**
- Personalized study recommendations based on subject readiness scores.
- Pre-sortie knowledge checks tied to the specific lesson planned for that day.
- Adaptive quiz difficulty based on cadet's historical quiz performance.
- Parent/guardian notification (for younger cadets) when inactivity exceeds 14 days.
