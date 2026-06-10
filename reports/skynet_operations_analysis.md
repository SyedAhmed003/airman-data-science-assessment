# Skynet Operations Analysis
**Project:** AIRMAN Aeronautics – Skynet + TOGA Assessment  
**Date:** 2026-06-10  

---

## 1. Aircraft Utilization

| Aircraft | Registration | Type | Available Hrs | Flown Hrs | Utilization % | Downtime Hrs | Defects |
|----------|-------------|------|--------------|-----------|--------------|-------------|---------|
| A001 | VT-ABC | C172 | 180 | 7.5 | 4.2% | 24 | 3 |
| A002 | VT-SKY | PA28 | 160 | 4.5 | 2.8% | 48 | 8 |
| A003 | VT-AIR | DA40 | 150 | 3.0 | 2.0% | 60 | 10 |

**Base-wise Utilization:**
- **B01 (VT-ABC + VT-SKY):** Average utilization ~3.5%
- **B02 (VT-AIR):** Utilization 2.0% — severely underutilized

**Key Findings:**
- All three aircraft are significantly underutilized (all below 10%), indicating either low cadet intake, high cancellations, or data window being small (15 sorties over ~1.5 weeks).
- VT-AIR (A003) has the worst combination: highest defect count (10), highest maintenance downtime (60 hrs), and lowest utilization.
- VT-ABC (A001) is the most reliable aircraft with only 3 defects and 24 hrs downtime.

**Aircraft Requiring Operational Review:**
- **A002 (VT-SKY):** 8 defects, 48 hrs downtime. May need scheduled maintenance review before further operations.
- **A003 (VT-AIR):** 10 defects, 60 hrs downtime (40% of available time). Strong candidate for grounding and full maintenance inspection.

---

## 2. Instructor Utilization

| Instructor | Base | Qualified On | Duty Hrs | Flight Hrs | Flight/Duty Ratio |
|-----------|------|-------------|---------|-----------|-----------------|
| Capt Rao | B01 | C172 | 145 | 82 | 56.5% |
| Capt Menon | B01 | PA28 | 160 | 96 | 60.0% |
| Capt Sharma | B02 | DA40 | 110 | 52 | 47.3% |

**Key Findings:**
- **Capt Menon (I002):** Highest flight/duty ratio at 60.0% — approaching overload risk if intake grows.
- **Capt Rao (I001):** 56.5% ratio — well-balanced workload.
- **Capt Sharma (I003):** Lowest flight hours (52 hrs) but also lowest duty hours. Underutilized at B02, directly linked to A003's high cancellation rate.
- **Qualification Mismatch Risk:** Each instructor is qualified on only one aircraft type. If an aircraft goes unserviceable, the associated instructor has zero sortie coverage. This is a single-point-of-failure risk for B02.

---

## 3. Dispatch Reliability

| Metric | Value |
|--------|-------|
| Total Sorties | 15 |
| Completed | 10 (66.67%) |
| Cancelled | 5 (33.33%) |
| Delayed (completed but late) | 7 |
| Average Delay (completed sorties) | 14.5 minutes |

**Cancellation Reasons:**
- **Weather:** 2 cancellation(s)
- **Aircraft Defect:** 2 cancellation(s)
- **Instructor Unavailable:** 1 cancellation(s)

**Key Findings:**
- Aircraft Defect is the single largest cancellation cause, accounting for 2 of 5 cancellations in the original dataset — directly tied to A003's reliability issues.
- Weather cancellations (2 instances) affect B01 operations — a normal risk factor but worth tracking seasonally.
- 1 cancellation due to Instructor Unavailability — low risk currently but needs monitoring as fleet grows.
- Average delay of ~20 minutes among completed sorties — manageable but adds cumulative scheduling pressure.

**Delay Trend by Lesson Type:**
- Navigation sorties show highest average delay (~28 min) — likely due to pre-flight planning complexity.
- Circuit sorties: moderate delays (~10 min average).
- General Handling: minimal delays when they do fly.
