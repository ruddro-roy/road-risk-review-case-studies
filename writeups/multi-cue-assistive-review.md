# Multi-cue assistive review

Short note on what the case study proofs show.

## Problem

Fleet and personal safety tools often flag too much. Managers spend time dismissing noise. The useful signal is timing: when risk rises, what cues fired, and whether there was lead time before contact.

## Approach

Run several independent detectors on each sampled frame. Fuse their cues into a timeline with explicit phases. Burn labels into a proof export so a reviewer can step through the same seconds the system used.

## What the two clips exercise

**FD1 (dashcam):** Cross-traffic entry. System reports moderate advance warning ~0.6 s before conflict at 32.5 s.

**PB5 (helmet):** Sustained high risk from early frames. No isolatable advance warning claimed. Imminent band in the last 2 s before conflict at 8.47 s.

Different shapes of the same pipeline: one clip with lead time, one without a clean rising edge.

## Status

Research prototype. Confidence scores are not yet calibrated to a measured true-positive rate. Two public clips only. Not a fleet evaluation.

Proof files: [results.md](../results.md). Caveats: [limitations.md](../limitations.md).