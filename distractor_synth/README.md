# Composited-distractor robustness test (30 Aug 2026)

Tests both detectors against synthetic distractor-bearing terrain, answering
the concern that the target-free FPR flights were flown over ground clear of
clutter.

Method
- Distractor objects (crumpled paper) were cropped from the assessment
  imagery at the matching altitude: hand-vetted picks from the 10 m and 15 m
  noise frames (their polygon-format labels did not suit box-based automated
  extraction), automated extraction from the 40 m frame (box labels). Patches in
  `patches/` (12 / 10 / 8 usable at 10 / 15 / 40 m after mask validation).
- Alpha mask per patch = largest bright low-saturation component, dilated 2,
  Gaussian-feathered, so only the object transfers (no background halo).
- Pasted at one distractor per cell-equivalent (1 / 2 / 13 per frame at
  11 / 15 / 40 m) at random non-overlapping positions, random flips,
  seed 42. Paste centres in `*_gt.json`.
- Inference replicated the original pipelines exactly: transfer-trained
  best.pt via yolov9 detect.py at 1920 px conf 0.01 (labels in `results/`);
  scratch-trained scratch_best.pt via ultralytics at 640 px (boxes with
  conf >= 0.05 in `scratch_runs_conf05.json`). Settings validated by
  re-running the clean 40 m frames: FPR 0.0288 vs published 0.029.
- A paste counts as flagged if a detection centre falls within its box
  (centre-in-box criterion, as in the recall assessment).

Results: `summary.json`; reported in Section 3.2 of the manuscript.
