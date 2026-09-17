# Fly High or Fly Low? — Dataset

Field imagery, annotations, detector weights, and detector predictions for the
paper **"Fly High or Fly Low? Selecting Time-Efficient UAV Search
Strategies for High-Recall Aerial Detection"** (Loewenich, Maire, Sandino,
Gonzalez; published open access in *Remote Sensing* **2026**, *18*(18), 3129 — https://doi.org/10.3390/rs18183129). Companion to the simulation
code at https://github.com/roguebytes/uav-survey-strategy-simulation.

All imagery: DJI Mini 4 Pro, 4032 x 2268 stills, ISO 100 (a small minority of
target-free frames at ISO 110), captured while hovering at waypoints. GPS
position tags have been removed from all released images; the drone-reported
relative altitude is retained.

The manuscript's two detectors are both YOLOv9-C models fine-tuned from
COCO-pretrained weights on the same target class (white 16 cm bowls) and are
named after the survey altitudes at which they operate: the **15 m detector**
(trained on imagery whose background does not match the mission terrain) and
the **40 m detector** (trained on imagery of the mission terrain itself).

## Contents (in this repository)

| Path | Description |
|---|---|
| `training/grass_tiles_260421/` | The 40 m detector's fine-tuning set: 390 tiles (300 train / 90 val, 672 x 453, 6 x 5 grid per source image, split by source image) carrying 214 bowl instances, tiled from 13 images captured 21 Apr 2026 over the mission terrain at 6 m to 65 m. |
| `assessment/noise_field/` | 22 Apr 2026 target-and-distractor field: one frame per altitude bin (14 bins, 5 m to 31 m; 16 frames). 16 bowls as targets with ground truth per frame; crumpled-paper distractor objects are present but deliberately unlabelled. Low-altitude bins use polygon labels, high-altitude bins bounding boxes (YOLO format, class 0 = bowl). Supports the 15 m detector's assessment (Figure 2a). |
| `assessment/grass_ladder/` | 22 Apr 2026 altitude ladder over the same field: one frame per bin, 5 m to 65 m, distractors present, bounding-box ground truth (16 bowls per bin). Supports the 40 m detector's assessment under sliced inference (Figure 2b). |
| `assessment/high_altitude/` | 9/13 Apr 2026 ladder: one frame per bin (13 bins, 5 m to 65 m), 16 bowls on marker mats, bounding-box ground truth. Retained for provenance; not behind any figure in the revised manuscript. |
| `predictions/grass_ladder_epoch99.csv` | The 40 m detector's per-bin precision and recall on `assessment/grass_ladder/` under sliced inference (640 px tiles, 40% overlap), over the candidate-threshold sweep. Source of Figure 2b. |
| `predictions/fpr_caches_epoch99/` | The 40 m detector's per-frame sliced-inference detections on the target-free flights at 11 m (97 frames) and 40 m (168 frames). Source of the measured 40 m false-positive rate of 0.004 and of the two spurious detections at the 11 m operating threshold. |
| `predictions/plain_grass_transfer/` | The 15 m detector's outputs (YOLO label files with confidences) on the target-free flights at 11 m and 15 m. Source of the measured false-positive rates at 11 m and 15 m. |
| `predictions/noise_field_transfer/` | The 15 m detector's outputs on the assessment field. |
| `predictions/ft_grass_confs_260825.json` | Superseded: whole-image detection confidences of an earlier detector configuration (and a rejected training candidate) on the target-free flights. Retained for provenance; the manuscript's 40 m false-positive rate comes from `fpr_caches_epoch99/`. |
| `distractor_synth/` | The composited-distractor robustness test: vetted distractor patches, paste ground truth, detector outputs for both detectors (the epoch-99 caches in `results/` are the 40 m detector's), and summary (see its README). |
| `release_checksums.json` | SHA-256 checksums of the release assets below. |

## Release assets

Large files are attached to the GitHub release (they exceed ordinary
repository limits):

| Asset | Contents |
|---|---|
| `detector_40m_yolov9c_epoch99.pt` | The 40 m detector's weights (YOLOv9-C, fine-tuned on `training/grass_tiles_260421/`, best epoch of a 100-epoch schedule). |
| `fpr_11m.zip` | 97 target-free frames, 23 Aug 2026, 11 m, grass oval |
| `fpr_15m.zip` | 93 target-free frames, 23 Aug 2026, 15 m, same oval |
| `fpr_40m.zip` | 168 target-free frames, 25 Aug 2026, 40 m, same oval |

## See also

- [roguebytes/uav-survey-strategy-simulation](https://github.com/roguebytes/uav-survey-strategy-simulation): the Monte Carlo model and the decision table behind the paper.
- [roguebytes/uav-detect-and-track](https://github.com/roguebytes/uav-detect-and-track): a ROS 2 and Gazebo simulation that flies the survey-then-verify profile end to end with a YOLOv9-C detector.

## Licence

Released under CC BY 4.0 (see LICENSE). Please cite the manuscript when
using this data.
