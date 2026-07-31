# road-risk-review case studies

Public, reviewable evidence for a recorded-video road-risk analysis system. The
lead result is a paired night-driving positive and negative control from the
licensed Nexar Collision Prediction dataset. Both use the same pinned
BADAS-Open/V-JEPA 2 checkpoint, causal inputs, measured NVIDIA L4 timings,
score-blind scheduler, and frozen exploratory policy.

Human review required. Not ADAS, collision avoidance, or a live camera test.

## Paired night controls

### Labeled positive: confirmation

The raw 8 Hz attempt missed its 125 ms compute budget on all 58 samples. A
measured-latency, latest-window virtual-clock projection emitted at 4.00 Hz.
The frozen two-sample policy produced a confirmation at 4.13 s displayed time.

https://github.com/user-attachments/assets/ee68d1f1-ff35-4748-a135-f45fa1afffb5

[Artifacts](case-studies/nexar-night-positive-00962/) |
[manifest](case-studies/nexar-night-positive-00962/causal_replay_manifest.json) |
[poster](case-studies/nexar-night-positive-00962/causal_replay_poster.jpg)

### Labeled negative: false-positive confirmation

The raw 8 Hz attempt missed its 125 ms compute budget on all 71 samples. The
same projection emitted at 4.02 Hz. The same frozen policy also confirmed this
negative control at 4.87 s displayed time: a concrete false positive that
prevents a safety or readiness claim.

https://github.com/user-attachments/assets/7c27d5ab-f2a2-4af7-9598-0e7dea8d137d

[Artifacts](case-studies/nexar-night-negative-01169/) |
[manifest](case-studies/nexar-night-negative-01169/causal_replay_manifest.json) |
[poster](case-studies/nexar-night-negative-01169/causal_replay_poster.jpg)

| Control | Raw 8 Hz deadline result | Projected output rate | Frozen-policy result |
|---|---:|---:|---|
| Nexar positive `00962` | 0/58 met 125 ms | 4.00 Hz | Confirmation |
| Nexar negative `01169` | 0/71 met 125 ms | 4.02 Hz | False-positive confirmation |

The projection is a recorded, virtual-clock counterfactual built from measured
per-window L4 compute times. It is not wall-clock-paced inference and excludes
camera capture, source decode, resize, causal-window assembly, display, and
operating-system jitter. The score is uncalibrated. See
[causal-replay-method.md](causal-replay-method.md) and
[limitations.md](limitations.md).

## What is independently inspectable

Each Nexar case folder contains exactly seven reviewed artifacts:

- 1600x900 H.264 replay, 1280x720 web encode, and poster
- Full model evidence with exact revisions, hashes, inputs, samples, repeat-run
  result, and checkpoint-load audit
- Raw FIFO timing trace
- Latest-window causal projection
- Renderer manifest binding the evidence, trace, projection, policy, and media

## Historical demonstrations

The `FD1sacdeW8E` and `PB5bNj3dzEk` folders are older YouTube-derived
demonstrations. They remain available for continuity but are not the lead
measured causal-replay evidence and do not establish live performance. Their
rights and provenance differ from the Nexar controls. See [SOURCE.md](SOURCE.md).

## Other evidence

- [Detailed results](results.md)
- [Controlled deterministic scenarios](controlled-scenarios/)
- [Historical two-clip regression summary](evaluation/verification-summary.md)
- [Architecture](architecture-overview.md)

## Source, rights, and use boundary

The Nexar-derived controls retain the Nexar Open Data License and required
attribution. No dataset-derived material here is offered for sale or
redistribution for profit. Commercial redistribution requires prior written
consent from Nexar Inc. See [SOURCE.md](SOURCE.md),
[NEXAR_DATA_LICENSE.txt](NEXAR_DATA_LICENSE.txt), and [NOTICE.md](NOTICE.md).
