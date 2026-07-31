# Measured causal-replay results

The primary result is a paired positive and negative night-driving control from
the licensed Nexar Collision Prediction dataset. Both cases use the same
reviewed BADAS-Open 1.0.0 checkpoint on a pinned V-JEPA 2 ViT-L backbone, the
same causal preprocessing, and the same frozen `exploratory_v1` display policy.
The score is an uncalibrated collision-class score, not a real-world collision
probability.

## Labeled positive: `nexar-night-positive-00962`

Raw FIFO inference attempted one output every 125 ms (8 Hz). NVIDIA L4 total
compute was 250.01 ms median and 256.25 ms p95; 0 of 58 samples met the 125 ms
deadline. Raw 8 Hz therefore failed.

The measured-latency latest-window projection retained 30 of 58 source windows,
superseded 28 older ready windows without inspecting their scores, and emitted
at 4.003 Hz. Its frozen policy first confirmed at target time 4.00 s,
availability time 4.129 s, and 30 fps displayed time 4.133 s.

https://github.com/user-attachments/assets/ee68d1f1-ff35-4748-a135-f45fa1afffb5

[Replay](case-studies/nexar-night-positive-00962/causal_replay.mp4) |
[web encode](case-studies/nexar-night-positive-00962/causal_replay_web.mp4) |
[manifest](case-studies/nexar-night-positive-00962/causal_replay_manifest.json) |
[model evidence](case-studies/nexar-night-positive-00962/model_evidence.json) |
[raw timing trace](case-studies/nexar-night-positive-00962/causal_replay_trace.json) |
[projection](case-studies/nexar-night-positive-00962/causal_projection.json)

## Labeled negative: `nexar-night-negative-01169`

Raw FIFO inference attempted the same 125 ms cadence. NVIDIA L4 total compute
was 248.35 ms median and 254.06 ms p95; 0 of 71 samples met the deadline.

The same projection retained 37 of 71 source windows, superseded 34, and
emitted at 4.021 Hz. The same frozen policy produced a false-positive
confirmation at target time 4.75 s, availability time 4.850 s, and 30 fps
displayed time 4.867 s.

https://github.com/user-attachments/assets/7c27d5ab-f2a2-4af7-9598-0e7dea8d137d

[Replay](case-studies/nexar-night-negative-01169/causal_replay.mp4) |
[web encode](case-studies/nexar-night-negative-01169/causal_replay_web.mp4) |
[manifest](case-studies/nexar-night-negative-01169/causal_replay_manifest.json) |
[model evidence](case-studies/nexar-night-negative-01169/model_evidence.json) |
[raw timing trace](case-studies/nexar-night-negative-01169/causal_replay_trace.json) |
[projection](case-studies/nexar-night-negative-01169/causal_projection.json)

## Interpretation

This pair proves that the evidence path can bind real model output, measured GPU
timing, causal availability, scheduler decisions, policy state, and rendered
media into inspectable artifacts. It does not prove a useful alert system. The
negative confirmation is direct evidence that this checkpoint and policy are
not ready for driver-facing safety use.

The latest-window result is a virtual-clock projection using measured
per-window compute durations. It is not a wall-clock-paced or end-to-end live
test. Decode, resize, causal-window assembly, camera capture, display, and
operating-system jitter are excluded from the timing claim.

## Historical YouTube demonstrations

Two older examples remain in the repository:

- [`FD1sacdeW8E`](case-studies/FD1sacdeW8E/): dashcam cross-traffic incident
- [`PB5bNj3dzEk`](case-studies/PB5bNj3dzEk/): helmet-camera low-side incident

They show earlier temporal and deterministic review presentation. They are
historical demonstrations, not part of the paired Nexar control result and not
evidence of live performance. See [SOURCE.md](SOURCE.md) for their separate
rights context.

## Limits

See [causal-replay-method.md](causal-replay-method.md) and
[limitations.md](limitations.md). Human review required. Not ADAS.
