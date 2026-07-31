# Measured causal-replay method

## Question

Can the reviewed BADAS-Open/V-JEPA 2 inference path produce causally available
temporal evidence at an attempted 8 Hz cadence, and what does a no-backlog
latest-window scheduler do to the output?

The paired test uses one Nexar-labeled positive and one Nexar-labeled negative.
Publishing the negative under the same frozen policy makes the principal
failure visible rather than selecting only a successful-looking clip.

## Fixed inputs and model

- BADAS-Open 1.0.0 at repository commit
  `01368cf5a164a576ae46eae3baf544e4ecdb2946`
- V-JEPA 2 ViT-L base revision
  `4aa02df83918538fc21cfaf576382fa20e489a80`
- BADAS checkpoint revision
  `8fda93711e79d72401b0a4efc151b56455885cd2`
- Checkpoint SHA-256
  `6b1ba91504542582412fee5100a17d6e06c87cb09619efec2efc34484f7042aa`
- Float32 inference on NVIDIA L4, fixed seed `20260731`
- 16 RGB frames at 256x256 sampled over a two-second causal context
- Attempted target cadence: 8 Hz, one target every 125 ms

Exact revisions, packages, preprocessing, input hashes, and direct scores are
in each `model_evidence.json`.

## Raw timing test

The first pass processed all target windows in FIFO order and measured
preprocessing, host-to-device transfer, GPU forward, and total compute for each
window. Decode, resize, causal-window assembly, camera capture, display, and
operating-system jitter were outside the measured interval.

The positive p95 total compute time was 256.25 ms; the negative p95 was
254.06 ms. No measured sample met 125 ms. The attempted raw 8 Hz cadence failed.

## Latest-window projection

The projection reuses the measured compute durations in a virtual clock. When
compute becomes free, it selects the newest unprocessed window whose input is
causally ready and marks older ready windows as superseded. It permits one
in-flight window and one newest pending window. Selection is score-blind.

This answers a bounded scheduler question: what the measured run would look
like without an accumulating FIFO backlog under those assumptions. It is not a
wall-clock-paced inference run, an end-to-end deployment measurement, or proof
that a camera system can sustain the projected rate.

## Frozen exploratory policy

The display threshold is 0.80. After at least one emitted low score, two
successive emitted scores at or above threshold within 0.5 seconds produce a
confirmation. A high sequence that begins before any observed low is labeled
sustained high with no observable onset. Scores are uncalibrated and the policy
is not validated for ADAS.

Applied without retuning:

| Case | Projected rate | Result |
|---|---:|---|
| Nexar positive `00962` | 4.003 Hz | Confirmation at 4.133 s displayed time |
| Nexar negative `01169` | 4.021 Hz | False-positive confirmation at 4.867 s displayed time |

## Replay integrity

Only outputs with `available_t_s <= displayed source time` are shown. The score
is held until a new output becomes available; it is not interpolated from a
future output. Plot positions use availability time. Reviewed recap information
appears after playback, not as future information during the replay.

Each manifest contains SHA-256 bindings for the media and its evidence chain.
The full model scoring pass was repeated and matched exactly within the stated
tolerance for these inputs.

## Conclusion boundary

The evidence chain and causal display mechanism work as an auditable research
artifact. The paired result does not validate a collision-warning product. The
negative confirmation, incomplete end-to-end timing, and two-clip sample make
human review mandatory and safety claims inappropriate.

Source and license: [SOURCE.md](SOURCE.md) and
[NEXAR_DATA_LICENSE.txt](NEXAR_DATA_LICENSE.txt). Full caveats:
[limitations.md](limitations.md).
