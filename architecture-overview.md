# Architecture overview

Conceptual layout of the private road-risk-review product beta. No implementation detail here.

```
  upload clip
       |
       v
  analysis worker  ---->  pluggable detectors (visibility, motion, lane,
       |                   proximity, VRU, surface, objects)
       v
  cue fusion and scoring
       |
       v
  flagged events + investigation pack
       |
       v
  temporal evidence renderer  ---->  reviewed public artifacts
       |
       v
  review UI (desktop)
```

**Detectors** run independently. Each returns cues with a confidence. None is trusted alone.

**Fusion** groups cues across frames, estimates conflict timing, and assigns incident phases (pre_conflict, conflict, post_impact).

**Evidence rendering** synchronizes the source window with fused risk, cue
channels, residual optical-flow saliency, a motion-centroid trail, incident
phase, and the reviewed conflict marker. The public manifest records which
channels were active.

**Learned-model slot** is optional. A future V-JEPA/BADAS run must enter through
a versioned probability-curve contract. If that curve is absent, the renderer
uses the words "fused risk evidence" and makes no learned-model claim.

**Output** is assistive: labeled timestamps, charts, videos, and exportable
review artifacts. A human decides what the footage shows.

Recorded clips only in the current beta. Live feed is planned separately.

See [limitations.md](limitations.md).
