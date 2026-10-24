# Classical Computer Vision Vehicle Counter

This project counts vehicles in traffic videos captured by a static camera. It uses OpenCV and NumPy only, with a deterministic, classical computer-vision pipeline and no trained or deep-learning models.

![Vehicle-counting workflow](assets/workflow.png)

## Features

- Detects day and night conditions automatically
- Builds a temporal-median background model for motion extraction
- Calibrates an angled virtual tripwire from road geometry
- Detects cars and motorcycles using contour geometry and Sobel texture checks
- Tracks vehicles across frames with velocity-based centroid matching
- Counts each tracked vehicle once when it crosses the tripwire

## How It Works

1. A temporal-median background model is created from sampled video frames.
2. Each frame is compared with the background to produce a motion mask.
3. Contours are filtered by size, shape, and horizontal-edge texture.
4. Valid detections are associated with persistent vehicle tracks.
5. A vehicle is counted once when its track crosses the calibrated tripwire.

## Requirements

- Python 3
- OpenCV
- NumPy

Install the dependencies:

```bash
pip install -r requirements.txt
```

## Usage

```python
from main import Solution

counter = Solution()
count = counter.forward("path/to/traffic_video.mp4")

print(f"Total vehicles: {count}")
```

`forward()` returns the total vehicle count as an integer. It returns `0` if the video cannot be opened or no vehicles cross the tripwire.

## Repository Structure

```text
CustomVehicleCounter/
├── assets/             # Sample videos and workflow image
├── main.py             # Vehicle-counting implementation
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```
