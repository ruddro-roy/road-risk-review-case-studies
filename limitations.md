# Limitations

Human review required. This work is not ADAS, collision avoidance, or a
substitute for driver or rider judgment. False positives and false negatives
are expected.

## Measured causal replay

- Raw float32 BADAS-Open inference on the NVIDIA L4 did not sustain the attempted
  8 Hz cadence. Every positive and negative sample missed the 125 ms compute
  deadline.
- The reported 4.00 Hz and 4.02 Hz rates are produced by a deterministic
  virtual-clock projection using measured per-window compute times. The test was
  not wall-clock paced and is not an end-to-end live camera benchmark.
- Measured compute excludes camera capture, source decode, resize,
  causal-window assembly, display, and operating-system jitter. Adding those
  costs can only worsen end-to-end latency.
- The scheduler keeps one in-flight window and chooses the newest causally ready
  unprocessed window without reading its score. This avoids an ever-growing FIFO
  backlog but discards older ready windows.
- Scores use zero-order hold until the next projected output becomes available.
  A replay frame never reads a future output.
- The `exploratory_v1` threshold and two-sample confirmation rule are frozen for
  this pair but are unvalidated and uncalibrated.
- The labeled negative produced a false-positive confirmation. This directly
  blocks a safety-readiness, reliable-alert, or collision-warning claim.
- Two short night clips do not estimate sensitivity, specificity, calibration,
  subgroup performance, robustness, or fleet false-positive rate.

## Learned temporal model

- The BADAS-Open collision-class score is not a probability of a real-world
  collision.
- A frozen checkpoint can learn dataset-specific cues that fail under new
  cameras, roads, lighting, geography, compression, weather, or road-user mix.
- Repeat-run equality checks deterministic execution for these inputs; it does
  not validate the model's semantics or generalization.
- No alert timing result here is a validated advance-warning lead time.

## Recorded-video pipeline

- All examples are recorded clips, not live feeds.
- Heavy compression, low resolution, low light, camera shake, unusual mounts,
  occlusion, glare, rain, and reflections can degrade multiple cues together.
- Residual optical-flow saliency in historical videos is not model attention.
  A motion-centroid trail is not object tracking, and a fixed ego corridor is
  not lane or path prediction.
- Visual wet-road cues are not friction measurements. Proximity cues are not
  physical distance. Geometry estimates are not steering guidance.

## What this repository does not prove

- Safe or useful real-time driver assistance
- Production latency, availability, or hardware suitability
- Legal admissibility, fault assignment, or regulatory compliance
- Generalization beyond the published clips
- Permission for commercial redistribution of Nexar-derived material
