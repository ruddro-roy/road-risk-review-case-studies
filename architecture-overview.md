# Architecture overview

Conceptual layout of the private road-risk-review prototype. No implementation detail here.

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
  review UI (desktop)
```

**Detectors** run independently. Each returns cues with a confidence. None is trusted alone.

**Fusion** groups cues across frames, estimates conflict timing, and assigns incident phases (pre_conflict, conflict, post_impact).

**Output** is assistive: labeled timestamps, charts, and exportable review artifacts. A human decides what the footage shows.

Recorded clips only in the current beta. Live feed is planned separately.

See [limitations.md](limitations.md).