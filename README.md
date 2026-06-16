# UPT Dataset

**UAV Person Tracking (UPT)** is a trajectory dataset created for human motion analysis and forecasting from UAV videos. It was designed to capture challenges that are common in real drone imagery, including platform motion, oblique viewing angles, resolution changes, noisy detections, and non-smooth pedestrian trajectories.

> This repository contains the original trajectory files extracted from UAV videos. Each trajectory is stored as a CSV file and represents the center coordinates of one tracked pedestrian over time.

## Overview

The dataset was created to support research on trajectory prediction in realistic UAV scenarios. Unlike many traditional pedestrian trajectory benchmarks, UPT focuses on situations with a non-stationary camera and oblique views, which are inherent to aerial video capture.

The associated study used UPT to evaluate forecasting methods based only on bounding box center coordinates rather than full image content. This repository, however, provides only the original CSV trajectories extracted from the videos.

## What this repository contains

- UAV video-derived pedestrian trajectories from real-world outdoor scenes.
- More than one hour of original video data captured at 24 FPS.
- Individual CSV files, each corresponding to a single tracked pedestrian trajectory.
- Bounding box center coordinates `(x, y)` recorded over time.
- Frame width and height values stored together with the coordinates to support later normalization and analysis.

## Dataset creation pipeline

<p align="center">
  <img src="https://github.com/rdmhora/UPT-Dataset/tree/main/images/pipeline.png" alt="UPT pipeline" width="900">
</p>

The UPT dataset was constructed through the following pipeline:

1. **Video acquisition**  
   UAV videos were recorded in real-world scenes using a moving aerial platform, with pedestrians walking naturally in open environments.

2. **Person detection and tracking**  
   Human instances were detected with YOLOv12-m, and identity consistency across frames was maintained with the tracking mechanism provided by the YOLO framework, which incorporates Kalman Filter-based tracking.

3. **Trajectory extraction**  
   For each detected pedestrian in each frame, the center of the bounding box was extracted. These image-space coordinates were used as the trajectory representation.

4. **CSV generation**  
   Each pedestrian trajectory was saved as an individual CSV file. In addition to the center coordinates, frame dimensions were stored to make later normalization possible.

## File format

Each CSV file represents a single pedestrian trajectory.

A typical file may contain fields such as:

| Column | Description |
|---|---|
| `frame` | Frame index |
| `x` | Bounding box center x-coordinate |
| `y` | Bounding box center y-coordinate |
| `width` | Frame width |
| `height` | Frame height |

If your repository uses a different naming convention, update the table above to match the actual CSV schema.

## Important note

This repository distributes the original 24 FPS trajectory CSV files only. Additional temporal resampling used in the associated paper was part of the experimental protocol and is not included here.

## Research motivation

Human trajectory prediction from UAV imagery is difficult because the camera is moving, the viewpoint is often oblique, and the target trajectories may include abrupt direction changes, partial occlusions, and detection noise.

UPT was introduced to better represent these conditions and to provide a benchmark for methods that operate only on coordinate sequences. This makes the dataset especially relevant for resource-constrained applications where full image-based reasoning may be too expensive.

## Repository structure

A simple GitHub structure for this dataset can look like this:

```text
UPT/
├── README.md
├── data/
│   ├── CSV/
│   └── CSV_test/
├── images/
│   ├── pipeline.png
│   ├── dataset_examples.png
│   └── trajectories.gif
└── LICENSE
```

The folder CSV contains the trajectories used for train and validates the models. The CSV_test contais the trajectories used for testing.



## Suggested README customization

You may want to adapt this README with the following repository-specific details:

- A short note about whether the original UAV videos are public or whether only the extracted trajectories are released.
- A license section describing how the dataset may be used.
- A citation section for the associated paper.
- A short description of the exact CSV columns used in this repository.
- A sentence describing the capture location or scene diversity, if you want to make the repository page more informative.

## Citation

If this dataset is used in academic work, please cite the associated paper describing the UPT dataset and its benchmark study.

---

