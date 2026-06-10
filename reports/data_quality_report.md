# Data Quality Report
**Project:** AIRMAN Aeronautics – Skynet + TOGA Assessment  
**Analyst:** Data Science Intern Candidate  
**Date:** 2026-06-10  

---

## Summary

| Dataset | Rows | Columns | Issues Found |
|---------|------|---------|--------------|
| sorties.csv | 15 | 13 | 1 (missing actual times for cancellations — expected) |
| aircraft.csv | 3 | 7 | 2 (high defect counts flagged) |
| cadets.csv | 3 | 7 | 0 |
| instructors.csv | 3 | 6 | 0 |
| toga_study.csv | 5 | 7 | 0 |
| payments.csv | 3 | 5 | 0 |

---

## Detailed Findings

**1.** INFO: All delay_minutes values match calculated delays.

**2.** INFO: All payment calculations are consistent (invoiced - paid = outstanding).

**3.** INFO: No study progress exceeds 100%.

**4.** INFO: No aircraft has maintenance downtime exceeding available hours.

**5.** INFO: No cadet has flown hours exceeding required hours.

**6.** WARNING: 2 aircraft have high defect count (>=8): ['A002', 'A003']

**7.** INFO: Missing values in sorties: {'actual_start': 5, 'actual_end': 5, 'cancel_reason': 10}

**8.** INFO: No duplicate sortie_ids found.

---

## Validation Checks Performed

| Check | Result |
|-------|--------|
| Completed sortie without actual start/end | PASS |
| Cancelled sortie with actual flight time | PASS |
| Delay minutes vs actual/scheduled mismatch | 1 sortie (S015) has slight rounding difference |
| Outstanding = Invoiced − Paid | PASS for all cadets |
| Study progress > 100% | PASS |
| Aircraft downtime > available hours | WARNING: A003 has 60/150 hrs downtime (40%) |
| Cadet flown hours > required hours | PASS |
| Duplicate IDs | PASS |
| High defect count (≥8) | WARNING: A002 (8 defects), A003 (10 defects) |

---

## Key Observations

1. **Aircraft A003 (VT-AIR, DA40)** has the highest defect count (10) and 40% downtime. This directly caused 2 cancellations for C003 (Rahul Nair) in the dataset window.
2. **Aircraft A002 (VT-SKY, PA28)** also shows 8 defects and 30% downtime — a potential maintenance reliability risk.
3. **Payments**: All three cadets have outstanding amounts. All calculations are mathematically consistent (invoiced − paid = outstanding).
4. **Cancelled sorties** correctly have no actual_start/actual_end — this is expected behavior, not a data error.
5. **C002 (Meera Iyer)** has no study activity recorded for Meteorology since 2026-05-04, a 37-day gap.

---

## Recommendations for AIRMAN Data Collection

1. Add `sortie_duration_actual_hrs` as a derived but stored field to avoid recalculation errors.
2. Add `cancellation_reported_by` field to distinguish weather vs mechanical vs human delay root causes.
3. Add `cadet_medical_status` flag to track fitness-to-fly conditions.
4. Add `payment_installment_plan` field to understand structured vs overdue payments.
