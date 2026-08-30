# Fly High or Fly Low? — Dataset

Field imagery, annotations, and detector predictions for the manuscript
**"Fly High or Fly Low? Selecting Time-Efficient UAV Search Strategies for
High-Recall Aerial Detection"** (Loewenich, Maire, Sandino, Gonzalez;
submitted to *Remote Sensing*, 2026). Companion to the simulation code at
https://github.com/roguebytes/uav-survey-strategy-simulation.

All imagery: DJI Mini 4 Pro, 4032 x 2268 stills, ISO 100 fixed, captured
while hovering at waypoints. GPS position tags have been removed from all
released images; the drone-reported relative altitude is retained.

## Contents (in this repository)

| Path | Description |
|---|---|
| `assessment/noise_field/` | 22 Apr 2026 target-and-distractor field: one frame per altitude bin (14 bins, 5 m to 31 m; 16 frames). 16 white bowls (16 cm) as targets, with ground truth per frame; crumpled-paper distractor objects are present but deliberately unlabelled. Low-altitude bins use polygon labels, high-altitude bins bounding boxes (YOLO format, class 0 = bowl). Supports the transfer-trained detector's assessment (Figure 2a). |
| `assessment/high_altitude/` | 9/13 Apr 2026 ladder: one frame per bin (13 bins, 5 m to 65 m), 16 bowls on marker mats, bounding-box ground truth. Supports the scratch-trained detector's assessment (Figure 2b). |
| `predictions/plain_grass_transfer/` | Transfer-trained detector outputs (YOLO label files with confidences) on the target-free flights at 11 m and 15 m. Source of the measured false-positive rates at 11 m and 15 m. |
| `predictions/noise_field_transfer/` | Transfer-trained detector outputs on the assessment field. |
| `predictions/ft_grass_confs_260825.json` | Scratch-trained (and a rejected transfer candidate's) detection confidences on the target-free flights. Source of the 40 m false-positive rate. |
| `distractor_synth/` | The composited-distractor robustness test: vetted distractor patches, paste ground truth, detector outputs, and summary (see its README). |
| `release_checksums.json` | SHA-256 checksums of the release-asset zips below. |

## Target-free imagery (release assets)

The full-resolution target-free flights are attached to the GitHub release
as zip archives (they exceed ordinary repository limits):

| Asset | Frames | Flight |
|---|---|---|
| `fpr_11m.zip` | 97 | 23 Aug 2026, 11 m, grass oval |
| `fpr_15m.zip` | 93 | 23 Aug 2026, 15 m, same oval |
| `fpr_40m.zip` | 168 | 25 Aug 2026, 40 m, same oval |

## Licence

Released under CC BY 4.0 (see LICENSE). Please cite the manuscript when
using this data.
