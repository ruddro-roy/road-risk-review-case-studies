# Verification summary

Regression check on the two case studies in this repository. Generated 2026-06-04. Mode: quick. Gate: PASS.

Both clips: committed timing summaries match frozen baselines (conflict time, duration, bands).

## FD1sacdeW8E (dashcam T-bone)

| Check | Result |
|-------|--------|
| conflict_s | 32.500 s |
| duration_s | 38.533 s |
| fusion_onset_s | 1.000 s |
| peak_risk | 0.958 |
| advance_warning_lead_s | 0.600 s |
| advance_warning_band | moderate |

## PB5bNj3dzEk (helmet low-side)

| Check | Result |
|-------|--------|
| conflict_s | 8.467 s |
| duration_s | 10.900 s |
| fusion_onset_s | 3.067 s |
| peak_risk | 0.971 |
| advance_warning | none claimed |
| imminent_start_s | 6.467 s |
| imminent_end_s | 8.467 s |

## What this does not prove

Fleet false-positive rate, legal admissibility, or live ADAS performance.