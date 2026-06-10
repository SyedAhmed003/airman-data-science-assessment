# Executive Insight Report
**To:** AIRMAN Aeronautics Leadership  
**From:** Data Science Intern Candidate  
**Product Focus:** Skynet + TOGA  
**Date:** 2026-06-10  
**Data Window:** May 1–8, 2026 (15 sorties, 3 cadets, 3 instructors, 3 aircraft)

---

## 1. Top 5 Operational Insights

1. **Aircraft A003 (VT-AIR, DA40 at B02) is a reliability liability.** With 10 defects, 60 hours of maintenance downtime (40% of available time), and 2 direct sortie cancellations, this aircraft is actively preventing C003 from progressing through PPL. It needs an immediate full maintenance review or temporary grounding.

2. **Dispatch reliability is 67% across all sorties** — meaning 1 in 3 planned training flights does not take place. Industry best-practice FTO targets are typically 80–85% completion rates. This gap represents both revenue risk and student dissatisfaction.

3. **Aircraft utilization is critically low** — all three aircraft are operating below 5% of available hours in this data window. Even accounting for the short observation window, this reflects scheduling inefficiency and low cadet throughput at current enrollment levels.

4. **Capt Menon (I002) is the most flight-loaded instructor** at a flight/duty ratio of 60%, while Capt Sharma (I003) at B02 is underutilized at 47%. The aircraft reliability problem at B02 is suppressing Capt Sharma's productive flight time — a talent underutilization issue.

5. **Navigation sorties carry the highest delay risk** (average 27 min delay). Pre-flight briefing and planning standards for Navigation lessons should be tightened. A Skynet checklist module for pre-flight preparation could directly reduce these delays.

---

## 2. Top 5 Training Progress Insights

1. **Meera Iyer (C002, CPL) is the highest-priority training risk.** At 37% progress with 126 hours remaining and a flying rate of only 1.68 hrs/week, she is on a trajectory that would take 18+ months to complete her CPL — well beyond acceptable norms. Both operational disruptions and financial non-payment are compounding factors.

2. **Rahul Nair (C003, PPL) has a compound risk profile.** Aircraft reliability at B02 is the root cause of his slow progress (only 12 hrs in ~3.5 months). Without fixing A003 or offering cross-base training at B01, C003 cannot advance at an acceptable pace.

3. **Arjun Menon (C001, PPL) is on track** at 63.3% with ~16.5 hours remaining. At current pace, he should complete PPL within 13 weeks. Minor interventions on Meteorology study and delay reduction would keep him on course.

4. **General Handling and Circuit lessons have the highest cancellation rates.** These are foundational early-stage lessons — cancellations here disproportionately affect newer cadets (C003) and delay advancement to more complex lesson types.

5. **No cadet has a flying rate sufficient for rapid completion.** Even C001's rate of 1.3 hrs/week equates to roughly 1 sortie per week. Increasing sortie frequency to 2–3 per week would dramatically improve throughput and FTO revenue.

---

## 3. Top 3 TOGA Personalization Opportunities

1. **Subject-specific intervention alerts:** TOGA should detect when a cadet's quiz score in a subject falls below 55 and automatically generate a "Focus Mode" study plan for that subject, surfacing the weakest chapters first.

2. **Pre-sortie knowledge activation:** The night before a scheduled sortie, TOGA should push a 5-question quiz on the theoretical content relevant to the next day's lesson type (e.g., before a Navigation sortie → Meteorology and Navigation theory mini-quiz). This creates a study-to-flight feedback loop.

3. **Inactivity escalation workflow:** When a cadet hasn't opened TOGA in 7 days, send a push notification. At 14 days, notify the instructor. At 21 days, flag to CFI. This tiered intervention prevents the kind of 43-day gap seen with C003.

---

## 4. Top 3 Finance Risks

1. **C002 (Meera Iyer): ₹1,10,000 outstanding, 51 days since last payment.** For a CPL student with many hours remaining, total outstanding could grow to ₹3–4 lakhs if not addressed. This is the single highest financial risk in the FTO.

2. **C003 (Rahul Nair): 50% of course fee unpaid, 61 days since payment.** A cadet with half the course fee unpaid and the slowest training progress represents both financial exposure and dropout risk.

3. **Total FTO outstanding of ₹2,40,000 with a 72% collection rate** signals a systemic payment follow-up gap. For an FTO with 3 cadets, this is proportionally very high. Skynet must include automated payment reminders and a configurable training-hold threshold.

---

## 5. Product Recommendations for Skynet

1. **Financial Clearance Gate:** Before a sortie can be scheduled, Skynet should check whether the cadet's outstanding payment exceeds a configured threshold (e.g., ₹75,000). If exceeded, flag to admin — instructor can still override with a reason code.

2. **Aircraft Health Dashboard:** Real-time defect count, maintenance hours, and availability status for every aircraft. Auto-alert when defect count crosses a threshold (e.g., 7+ defects → maintenance review required flag).

3. **Sortie Completion Probability Score:** Using historical data on weather, aircraft status, instructor availability, and lesson type, Skynet should predict same-day cancellation probability and suggest proactive rescheduling.

4. **Instructor Workload Monitor:** Weekly duty-hour and flight-hour summaries with color-coded alerts (green/amber/red) to prevent instructor fatigue and regulatory violations.

5. **Base-level Operations Summary Report:** A weekly PDF/dashboard auto-generated for each FTO base showing utilization, completion rate, outstanding payments, and top 3 actions required.

---

## 6. Product Recommendations for TOGA

1. **Adaptive Study Planner:** Based on exam dates, current progress, and quiz scores, auto-generate a week-by-week study plan for each cadet showing exactly which chapters to cover each day.

2. **Flight-Theory Correlation View:** Show cadets a visual connecting their study readiness score in each subject to their flying lesson schedule. "You have a Navigation sortie in 3 days — your Winds & Weather chapter score is low. Study now?"

3. **Progress Health Score (Cadet View):** Surface a clean, motivating "Flight Readiness Score" to cadets (not the risk score) that rewards consistent study behavior, improving quiz scores, and completing chapters ahead of schedule.

---

## 7. Data Quality Issues Found

1. A003 has unusually high defect count (10) — may indicate inconsistent defect logging practices or a genuine maintenance backlog.
2. C003 has TOGA data for only 1 subject (Navigation) — other subjects may be missing from the dataset, understating study engagement.
3. Delay_minutes field is manually entered — small calculation mismatches found (S015) suggest it should be auto-calculated from actual times.
4. No sortie duration is stored directly — it must be derived, introducing potential for errors.

---

## 8. Suggested Next Data Fields for AIRMAN to Collect

| Field | Why It Matters |
|-------|---------------|
| `cadet_medical_certificate_expiry` | DGCA medical lapse immediately halts training |
| `sortie_debrief_score` | Instructor qualitative rating per sortie |
| `simulator_hours` | Part of CPL syllabus — missing = incomplete progress picture |
| `payment_plan_type` | Distinguishes planned installments from overdue payments |
| `weather_condition_at_takeoff` | Better cancellation root-cause analysis |
| `cadet_prior_flying_experience_hrs` | Baseline for progress expectation |
| `exam_registration_date` | Tracks theory exam pipeline |
| `aircraft_last_100hr_check_date` | More granular than defect count for maintenance risk |

---

## 9. Final Recommendation to AIRMAN Leadership

This analysis — even from a small 3-cadet, 15-sortie dataset — reveals a pattern that likely exists at scale across Indian FTOs: **operational, financial, and educational risks cluster together in the same cadets.** The cadets who fly the least are also studying the least, paying the least, and experiencing the most aircraft-related disruptions.

Skynet and TOGA are uniquely positioned to break this cycle — not by simply reporting the problem, but by creating **proactive intervention workflows** that alert the right person (CFI, finance team, cadet) at the right time with the right action.

The risk scoring model built in this assessment should be the foundation of a **"Cadet Intelligence Layer"** that Skynet surfaces to FTO leadership and TOGA serves to cadets in an encouraging, personalized form.

With richer data (simulator hours, exam scores, medical status, payment plans), this model becomes production-ready and could be AIRMAN's strongest differentiator against generic FTO software.
