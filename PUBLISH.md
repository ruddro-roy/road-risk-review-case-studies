# Publish record

Local notes for syncing this public repo from the private `road-risk-review` project. Not for external readers.

## Paths

| Role | Path |
|------|------|
| Private source | `/Users/ruddroroy/Downloads/road-risk-review` |
| Public publish | `/Users/ruddroroy/Downloads/road-risk-review-case-studies` |
| Case study assets (private) | `docs/youtube_accident_analysis/<video_id>/` |

## Last published

- Date: 2026-06-09
- Clips: FD1sacdeW8E, PB5bNj3dzEk
- Source commit (private): dcdb9c2 (proprietary license)
- Verification snapshot: 2026-06-04 quick gate PASS

## Copy (media)

Per `<video_id>/`, copy:

- `detection_proof.mp4`, `detection_proof.gif`, `detection_proof_hd.mp4`
- `proof_poster.jpg`, `00_risk_timeline.png`, `10_sequence_strip.jpg`
- `conflict_moment.jpg`, `conflict_moment_annotated.jpg`
- `seq_00_-2.4s.jpg` through `seq_08_-0.0s.jpg`

## Do not copy

- `run.py`, `analyze.py`, `conflict_detect.py`, `download_clips.py`
- `per_frame.csv`, `driver_review.json`, raw `summary.json`
- `docs/architecture.md`, anything under `ml/`, `backend/`

## Redact before publish

- Write `summary.public.json` from timings only (no paths, thresholds, method_notes)
- Strip production pipeline and per-frame references from investigation reviews
- Sanitize `limitations.md` (no config paths or API names)
- Verification summary: PASS table only, no baselines paths

## Regenerate (private repo)

```bash
cd /Users/ruddroroy/Downloads/road-risk-review
python3 docs/youtube_accident_analysis/run.py
make verify-quick
```

Then re-copy media and update `evaluation/verification-summary.md` if timings changed.

## Push

```bash
cd /Users/ruddroroy/Downloads/road-risk-review-case-studies
git add -A
git commit -m "Update case study proofs"
git push origin main
```