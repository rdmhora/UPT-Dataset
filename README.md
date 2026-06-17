# UPT Dataset
![Raw Video](images/raw_image_gif.gif)
![Annotated Video](images/track_gif.gif)

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
  <img src="https://github.com/rdmhora/UPT-Dataset/blob/main/images/%E2%80%8Epipeline.png" alt="UPT pipeline" width="900">
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

The first row of the file contains the image dimensions, given as width and height.  
The second row contains the coordinate headers, `x` and `y`.  
From the third row onward, each row corresponds to one frame of the trajectory and stores the pedestrian position in image coordinates.  
The first column represents the horizontal coordinate (`x`), and the second column represents the vertical coordinate (`y`).

| Row | Content |
|---|---|
| 1 | Image dimensions: width and height |
| 2 | Column headers: `x`, `y` |
| 3 onward | Pedestrian coordinates for each frame |


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



## Dataset usage

The dataset is publicly available for research use.  
Users are free to use, share, and adapt the dataset for academic purposes, provided that the associated publication is properly cited.

## Citation

IIf you use this dataset, please cite:

```bibtex
@inproceedings{hora2026upt,
  author    = {Hora, Rafael D. M. and Santos, Daniel R. and Paulo, Maurício C. M. and Ferrari, Felipe and Feitosa, Raul Q. and Rosa, Paulo F. F.},
  title     = {Human Trajectory Prediction on UAV Images: A Comparative Study},
  booktitle = {Proceedings of the XXV ISPRS Congress},
  year      = {2026},
  address   = {Toronto, Canada}
}
```
---

