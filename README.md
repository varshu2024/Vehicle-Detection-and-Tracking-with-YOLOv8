# Vehicle Detection and Tracking with YOLOv8


## Overview

This repository contains a vehicle detection and tracking system using YOLOv8 (You Only Look Once version 8), a state-of-the-art object detection model. The system can detect and track vehicles in real-time from video streams or recorded videos, with options for counting vehicles and analyzing traffic patterns.

## Features

- Real-time vehicle detection using YOLOv8
- Multiple object tracking
- Vehicle counting (per frame and cumulative)
- Speed estimation (optional)
- Support for various input sources (video files, webcam, RTSP streams)
- Customizable detection thresholds
- Visualization of detection and tracking results
- Export results to CSV or JSON

## Prerequisites

Before you begin, ensure you have the following installed:

- Python 3.7 or higher
- pip package manager
- NVIDIA GPU (recommended for better performance) with CUDA and cuDNN (if using GPU acceleration)

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/vehicle-detection-yolov8.git
   cd vehicle-detection-yolov8
   ```

2. Create and activate a Python virtual environment (recommended):
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Basic Detection on a Video File

```bash
python detect.py --source path/to/your/video.mp4 --weights yolov8n.pt
```

### Real-time Detection from Webcam

```bash
python detect.py --source 0 --weights yolov8n.pt
```

### Tracking Vehicles

To enable tracking (using ByteTrack by default):

```bash
python detect.py --source path/to/video.mp4 --weights yolov8n.pt --track
```

### Available Arguments

| Argument          | Description                                      | Default Value       |
|-------------------|--------------------------------------------------|---------------------|
| `--source`        | Input source (file path, 0 for webcam, RTSP URL) | '0' (webcam)        |
| `--weights`       | Path to YOLOv8 model weights                     | 'yolov8n.pt'        |
| `--conf`          | Confidence threshold                             | 0.25                |
| `--iou`           | IOU threshold for NMS                            | 0.45                |
| `--imgsz`         | Inference size (pixels)                          | 640                 |
| `--device`        | Device to run on (cpu, 0, 1, ...)                | '' (auto-detect)    |
| `--show`          | Show results                                     | True                |
| `--save`          | Save results                                     | False               |
| `--classes`       | Filter by class (e.g., --classes 2 3 for cars)   | None (all classes)  |
| `--track`         | Enable tracking                                  | False               |
| `--count`         | Enable vehicle counting                          | False               |

## Customization

### Vehicle Classes

By default, the system detects these COCO classes relevant to vehicles:
- 2: car
- 3: motorcycle
- 5: bus
- 7: truck

You can specify which classes to detect using the `--classes` argument.

### Using Different YOLOv8 Models

You can use different YOLOv8 model sizes by changing the weights file:
- yolov8n.pt (nano)
- yolov8s.pt (small)
- yolov8m.pt (medium)
- yolov8l.pt (large)
- yolov8x.pt (extra large)

Download other models from the [Ultralytics YOLOv8 repository](https://github.com/ultralytics/ultralytics).

## Performance

Approximate performance on NVIDIA Tesla T4:

| Model   | FPS (640x640) | mAP50 |
|---------|--------------|-------|
| YOLOv8n | 120          | 0.37  |
| YOLOv8s | 80           | 0.44  |
| YOLOv8m | 45           | 0.49  |
| YOLOv8l | 30           | 0.52  |
| YOLOv8x | 20           | 0.53  |

## Output Examples

The system can generate:
- Annotated video with bounding boxes and tracking IDs
- CSV/JSON files with detection data (timestamps, coordinates, class, confidence)
- Vehicle count statistics

## Troubleshooting

1. **Slow performance**: Try using a smaller YOLOv8 model (e.g., yolov8n.pt) or reduce the inference size (--imgsz 320).
2. **CUDA errors**: Ensure you have the correct version of CUDA and cuDNN installed for your GPU.
3. **Missing dependencies**: Run `pip install -r requirements.txt` to ensure all packages are installed.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Ultralytics](https://ultralytics.com/) for YOLOv8
- [ByteTrack](https://github.com/ifzhang/ByteTrack) for object tracking
- [OpenCV](https://opencv.org/) for computer vision utilities

## Contact

For questions or suggestions, please open an issue or contact the maintainers.
