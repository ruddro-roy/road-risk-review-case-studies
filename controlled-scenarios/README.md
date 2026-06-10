# Controlled scenario evaluation

Deterministic kinematic road scenarios rendered through a pinhole camera model. This is an evaluation aid between synthetic unit stimuli and real road footage.

The reference timing comes from the analytic scene geometry. It is useful for checking conflict timing, early alert behavior, and false-conflict cases. It is not a driving simulator, not real-world validation, and not a performance claim.

## Files

- `scenario-results-grid.png` - all nine scenario outcomes in one visual summary.
- `timing-summary.json` - public timing summary using analytic reference timing.
- `clips/t_bone_45kmh.mp4` - cross-traffic conflict example.
- `clips/lead_brake_a7.mp4` - lead-vehicle braking conflict example.
- `clips/ped_near_miss_40kmh.mp4` - near-miss example currently flagged as a conflict.

## Current reading

The timing run detects all seven contact scenarios with a mean absolute conflict-time error of 0.194 s on this controlled set. It also flags both pedestrian near-miss scenarios as conflicts. That is an exposed limitation, not a product claim.

These files are public proof artifacts only. They do not expose the private implementation.
