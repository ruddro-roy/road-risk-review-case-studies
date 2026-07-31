# Incident case studies

Two segments from public YouTube uploads, used for educational research
demonstration. Temporal evidence is synchronized with the reviewed timeline.
Human review required. Not a benchmark. Source detail: [SOURCE.md](SOURCE.md).

Timings match the labels burned into each proof export at container FPS.

## Dashcam T-bone (ViralHog) (`FD1sacdeW8E`)

Conflict **32.50 s** | duration **38.53 s** | peak risk **0.96** | advance ~**0.6 s** (moderate)

**Footage:** Vehicle enters from the side for a T-bone style impact near 32.5 s.

**Output:** Risk crosses moderate band ~0.6 s before conflict. Phases: pre_conflict 31.9 to 32.5 s, conflict 32.5 s, post_impact 32.5 to 38.5 s.

**Learned evidence:** BADAS-Open/V-JEPA 2 rises from 0.11, peaks at
0.974, and first crosses its 0.80 display threshold at 32.125 s. That is
0.375 s before the reviewed conflict. This is an uncalibrated collision-class
score, not a probability of real-world collision.

https://github.com/user-attachments/assets/84d96a1d-a414-4b05-9ee4-0137d4d0b4df

[Versioned evidence video](case-studies/FD1sacdeW8E/temporal_evidence.mp4) |
[poster](case-studies/FD1sacdeW8E/temporal_evidence_poster.jpg) |
[provenance](case-studies/FD1sacdeW8E/temporal_evidence_manifest.json) |
[model evidence](case-studies/FD1sacdeW8E/model_evidence.json) |
[per-frame data](case-studies/FD1sacdeW8E/summary.public.json)

Compact legacy overlay: [MP4](case-studies/FD1sacdeW8E/detection_proof.mp4) |
[GIF](case-studies/FD1sacdeW8E/detection_proof.gif) |
[timeline](case-studies/FD1sacdeW8E/00_risk_timeline.png) |
[review](case-studies/FD1sacdeW8E/investigation_review.md)

Full resolution: [detection_proof_hd.mp4](case-studies/FD1sacdeW8E/detection_proof_hd.mp4)

Source (context): https://www.youtube.com/watch?v=FD1sacdeW8E

## Motorbike low-side (helmet-mounted camera) (`PB5bNj3dzEk`)

Conflict **8.47 s** | duration **10.90 s** | peak risk **0.97**

**Footage:** Low-side loss of control with peak motion near 8.5 s.

**Output:** No isolatable advance-warning lead time. Imminent window 6.47 to 8.47 s. Phases: pre_conflict 1.0 to 8.47 s, conflict 8.47 s, post_impact 8.47 to 10.87 s.

**Learned evidence:** BADAS-Open/V-JEPA 2 is already above 0.94 at the
first model-covered sample and remains high. The score therefore supplies no
isolatable learned onset or lead-time claim for this clip.

https://github.com/user-attachments/assets/45bc5256-9a7d-4b79-8d50-940d4b51fb8b

[Versioned evidence video](case-studies/PB5bNj3dzEk/temporal_evidence.mp4) |
[poster](case-studies/PB5bNj3dzEk/temporal_evidence_poster.jpg) |
[provenance](case-studies/PB5bNj3dzEk/temporal_evidence_manifest.json) |
[model evidence](case-studies/PB5bNj3dzEk/model_evidence.json) |
[per-frame data](case-studies/PB5bNj3dzEk/summary.public.json)

Compact legacy overlay: [MP4](case-studies/PB5bNj3dzEk/detection_proof.mp4) |
[GIF](case-studies/PB5bNj3dzEk/detection_proof.gif) |
[timeline](case-studies/PB5bNj3dzEk/00_risk_timeline.png) |
[review](case-studies/PB5bNj3dzEk/investigation_review.md)

Full resolution: [detection_proof_hd.mp4](case-studies/PB5bNj3dzEk/detection_proof_hd.mp4)

Source (context): https://www.youtube.com/watch?v=PB5bNj3dzEk

## Evidence provenance

The colored saliency layer is residual optical flow after subtracting median
camera motion. It is not learned-model attention. The motion-centroid trail is
not an object identity. The ego corridor is a fixed review region, not a
predicted path.

The green curve is deterministic fused CV evidence. The cyan curve is the
separate reviewed BADAS collision-class score from a pinned V-JEPA 2 backbone.
Neither is a calibrated collision probability. Learned values are direct 8 Hz
samples; the 15 fps renderer interpolates only between adjacent samples for
display and never extrapolates beyond model coverage.

## Limits

[limitations.md](limitations.md)
