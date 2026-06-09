# Limitations

This is not ADAS, collision avoidance, or a substitute for driver or rider judgment. False negatives and false positives are expected. Wet or slippery road cues are visual proxies only, not friction measurement. Output is for human review only.

## Pipeline-wide

- Confidence values are not yet calibrated. A score of 0.7 is not a measured true-positive rate.
- Analysis applies to recorded clips, not live feeds.
- Heavy compression, low resolution, camera shake, or unusual mount angles can degrade every cue at once.

## Per detector

**Visibility:** Weak separation of low light vs underexposure. Cannot distinguish fog, condensation, and a dirty lens.

**Motion flow:** Sensitive to wipers, reflections, and mount shake. Edge motion is often artifact, not a road event.

**Lane curvature:** Geometry estimate from the lower frame band. Degrades on cobblestones, markings, and shadows. Not steering angle or surveyed road geometry.

**Lead proximity:** Closing proxy from object boxes or forward-region scale change. Not distance. Weak when the lead vehicle is occluded or enters from the side.

**VRU presence:** Person and bicycle classes when a model is active. Static shapes and parked bikes can false-positive. Heuristic fallback is experimental.

**Surface inference:** Visual proxy from reflections, spray, rain streaks, and low luminance. Not friction measurement. Always low confidence.

## Scoring

- Severity bands are bucketed from a continuous score. Near-boundary events may differ in band despite similar cues.
- Short events below the merge window can be dropped to reduce flicker.

## What this repo does not prove

- Fleet false-positive rate
- Legal admissibility or fault assignment
- Live safety-critical performance