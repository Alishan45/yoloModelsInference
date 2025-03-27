# YOLO-Based Object Tracking & Pose Estimation

This project implements **YOLO models** for real-time object tracking, segmentation, and pose estimation in videos. It supports **custom-trained models** and performs inference on **YouTube videos** or local files using tracking algorithms like **ByteTrack**.

## 🚀 Features
- **Object Detection, Segmentation, & Pose Estimation**
- **Real-time Tracking** with ByteTrack
- **Custom YOLO Model Support**
- **YouTube & Local Video Processing**
- **Auto-saving Results**

## 📌 Installation
First, install the required dependencies:
```bash
pip install ultralytics pytube opencv-python numpy yt-dlp
```

## 🔥 Usage
### 1️⃣ Load a YOLO Model
```python
from ultralytics import YOLO

# Load YOLO models
model_detect = YOLO("yolo11n.pt")   # Detection
model_seg = YOLO("yolo11n-seg.pt")  # Segmentation
model_pose = YOLO("yolo11n-pose.pt") # Pose Estimation
model_custom = YOLO("path/to/best.pt")  # Custom model
```

### 2️⃣ Perform Tracking
#### Using a YouTube Video
```python
results = model_detect.track("https://www.youtube.com/watch?v=VIDEO_ID", show=True, save=True, tracker="bytetrack.yaml")
```
#### Using a Local Video File
```python
results = model_detect.track("video.mp4", show=True, save=True)
```

### 3️⃣ Process Tracking Results
```python
for r in results:
    boxes = r.boxes  # Bounding boxes
    masks = r.masks  # Segmentation masks (if applicable)
    probs = r.probs  # Classification probabilities
```

## 🎥 Download YouTube Videos
If tracking on YouTube videos fails, download them first:
```python
from pytube import YouTube

yt_url = "https://www.youtube.com/watch?v=VIDEO_ID"
yt = YouTube(yt_url)
stream = yt.streams.filter(file_extension="mp4", res="720p").first()
stream.download(filename="video.mp4")
```
Or use `yt-dlp` (recommended):
```bash
yt-dlp -f "best[ext=mp4]" https://www.youtube.com/watch?v=VIDEO_ID -o video.mp4
```

## 🛠 Troubleshooting
- **Shorts videos not downloading?** Convert the link to `https://www.youtube.com/watch?v=VIDEO_ID`
- **YOLO not saving results?** Add `save=True` to `.track()`
- **Errors in YouTube downloads?** Use `yt-dlp` instead of `pytube`

## 📜 License
This project is licensed under the **MIT License**.

---
### 🌟 Star this repo if you find it useful! 🚀
