# Architecture overview

The public evidence separates model execution, scheduler projection, policy,
and presentation so each claim can be inspected independently.

```text
recorded licensed clip
        |
        v
causal 16-frame contexts at an attempted 8 Hz cadence
        |
        v
pinned BADAS-Open / V-JEPA 2 inference on NVIDIA L4
        |
        +--> reviewed model evidence: scores, revisions, hashes, repeat run
        |
        v
raw FIFO timing trace: measured compute and 125 ms deadline result
        |
        v
score-blind latest-ready scheduler (virtual clock, one in flight)
        |
        +--> emitted windows + explicitly superseded windows
        |
        v
frozen exploratory display policy
        |
        v
causal replay renderer + binding manifest
        |
        v
human review
```

## Evidence contract

`model_evidence.json` records exact model revisions, checkpoint hash, input
hash, causal preprocessing, direct samples, checkpoint-load audit, repeat-run
integrity, and review status.

`causal_replay_trace.json` records measured per-window preprocessing,
host-to-device transfer, GPU forward, and total compute times from the raw FIFO
run. It also records that the attempted 125 ms deadline was not met.

`causal_projection.json` applies a deterministic, score-blind,
work-conserving latest-ready scheduler to those measured durations. It is a
virtual-clock counterfactual, not a second live inference run.

`causal_replay_manifest.json` binds the evidence, trace, projection, policy,
render window, media hashes, transitions, causal guards, and limitations.

## Causal presentation boundary

During replay, only projected outputs whose `available_t_s` is at or before the
displayed source time are visible. History is placed by availability time and
scores are held, not interpolated from future values. Human-reviewed labels and
recap text appear only after the replay window.

## Private product boundary

The private product also contains deterministic cue extraction, fusion,
incident review, and export workflows. Those implementation details are not
published here. The older YouTube case folders show that historical path and
remain separate from the paired Nexar measured replay.

Recorded clips only. Human review required. Not ADAS.

See [causal-replay-method.md](causal-replay-method.md) and
[limitations.md](limitations.md).
