# 👣 Intelligent People Counting System (YOLOv8 + ByteTrack)

This project implements a **computer vision-based footfall counting system** that counts the number of people **entering and exiting** through a doorway, corridor, or gate in a video feed.

---

## 📋 Problem Statement

Develop a system that:

- ✅ Detects humans in each frame
- ✅ Tracks them across time
- ✅ Defines a virtual crossing line
- ✅ Counts entries and exits accurately
- ✅ Displays real-time visual feedback

---

## 🚀 Solution Overview

The system uses:

| Component | Purpose |
|----------|---------|
| **YOLOv8** | Human detection |
| **ByteTrack** | Multi-object tracking with ID consistency |
| **Smart Line Detection** | Automatically places counting line |
| **Crossing Logic** | Determines entry vs exit movement |

It supports:

- **Video Processing Mode** (pre-recorded videos)
- **Live Webcam Mode** (real-time people counting)

---

## ✨ Features

### ✅ Core Functionality
- YOLOv8-based human detection
- ByteTrack multi-object tracking
- Dynamic virtual line placement
- Bidirectional counting (Entry & Exit)
- Real-time annotated visualization

### ⭐ Bonus Enhancements
- Movement heatmap visualization
- CSV logging with timestamps
- Smart auto-optimized counting line
- Supports both video files and webcam streams

---

## 📊 Methodology

### 1️⃣ Smart Line Detection
- System analyzes early frames to determine movement direction
- If movement is mostly horizontal → **vertical counting line**
- If movement is mostly vertical → **horizontal counting line**

### 2️⃣ Detection & Tracking Pipeline
Frame → YOLOv8 Detection → ByteTrack Tracking → Unique Person ID → Position History

**Filtering Applied:**
- Confidence threshold ≥ 0.3
- Human aspect ratio check
- Minimum bounding box area

### 3️⃣ Counting Logic
```python
For each tracked person:
1. Compute centroid of bounding box
2. Determine which side of the line they are on
3. If side changes → person crossed line
4. Determine direction of crossing:
   - Left → Right / Top → Bottom = ENTRY
   - Right → Left / Bottom → Top = EXIT
5. Increment counters and prevent double-counting
