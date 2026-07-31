# road-risk-review case studies

Public proof for road-risk-review: deterministic computer vision and reviewed
BADAS-Open/V-JEPA 2 temporal evidence on recorded dashcam and helmet-camera
footage. Two worked examples use publicly available YouTube clips for an
educational research demonstration. Not ADAS. Not collision avoidance. Human
review required.

Source and rights: [SOURCE.md](SOURCE.md). Caveats: [limitations.md](limitations.md).

## Watch the evidence

### Dashcam cross-traffic conflict

Six seconds at true speed. The learned collision-class score rises from 0.11
and crosses the 0.80 display threshold at 32.125 s, 0.375 s before the reviewed
32.5 s conflict. The independent deterministic CV phase crosses its moderate
band 0.6 s before conflict.

https://github.com/user-attachments/assets/c0017b62-6e9c-4c84-a031-f2469d5e6316

### Helmet-camera low-side

The learned score is already above 0.94 at the first model-covered sample. The
video reports that sustained elevated response without turning it into a
six-second advance-warning claim.

https://github.com/user-attachments/assets/9952ac56-e99f-443e-9c19-321f65e7cc2d

These July 31, 2026 renders contain reviewed BADAS-Open 1.0.0 inference on a
pinned V-JEPA 2 backbone. Each clip has 49 direct predictions from causal
16-frame contexts at 8 Hz; a second run reproduced every score exactly. The
scores are uncalibrated, the colored heatmap remains residual optical flow,
and BADAS never controls the deterministic CV phase labels. Exact revisions,
input and checkpoint hashes, run IDs, sample hashes, and key-load audit are in
each case folder.

## Case studies

| Clip | Camera | Conflict | Notes |
|------|--------|----------|-------|
| [FD1sacdeW8E](case-studies/FD1sacdeW8E/) | Dashcam | 32.5 s | Advance warning ~0.6 s (moderate band) |
| [PB5bNj3dzEk](case-studies/PB5bNj3dzEk/) | Helmet | 8.47 s | No isolatable advance warning; imminent window 6.47 to 8.47 s |

Full writeup: [results.md](results.md)

Each folder contains the versioned 1600x900 evidence video, a lightweight web
encode, poster, public provenance manifest, reviewed model-evidence JSON,
compact legacy overlay, timeline chart, sequence strip, conflict stills,
investigation review, and redacted timing summary.

The players above are GitHub-native video attachments uploaded from the same
local H.264 files stored in the case folders. The versioned copies remain
available if an attachment URL is unavailable.

## Controlled scenarios

A small deterministic scenario set is published as an evaluation aid for conflict timing and false-conflict behavior: [controlled-scenarios/](controlled-scenarios/). It is not real-world validation.

## Evaluation

Regression gate for these two clips: [evaluation/verification-summary.md](evaluation/verification-summary.md)

## Architecture

High-level overview only: [architecture-overview.md](architecture-overview.md)

## Terms

[SOURCE.md](SOURCE.md) | [NOTICE.md](NOTICE.md)
