📋 Problem Statement
Develop a computer vision-based system that counts the number of people entering and exiting through a specific area (doorway, corridor, or gate) in a video.
Assignment Requirements:

✅ Detect humans in video frames
✅ Track their movements frame-by-frame
✅ Define a virtual line/ROI for counting
✅ Count entries and exits accurately
✅ Display counts in real-time

🚀 Solution Overview
This project implements an intelligent footfall counting system using YOLOv8 for detection and ByteTrack for tracking. The system works in two modes:

Video Processing Mode - Process recorded videos
Real-Time Mode - Live counting via webcam

✨ Features Implemented
Core Requirements ✅

Human Detection: YOLOv8 (COCO pre-trained)
Multi-Object Tracking: ByteTrack algorithm
Virtual Counting Line: Automatically determined based on movement analysis
Bidirectional Counting: Separate entry/exit counters
Real-time Visualization: Color-coded bounding boxes and live counts

Bonus Features ⭐

Movement Heatmap: Visual representation of traffic patterns
CSV Logging: Detailed event log with timestamps
Smart Line Detection: Auto-determines optimal line orientation
Live Webcam Support: Real-time processing capability

Upload or specify video file
System automatically processes entire video
Outputs: annotated video, heatmap, CSV log

## 📊 Methodology

### 1. Smart Line Detection

- Analyzes first 200 frames (or 10 seconds for live)
- Calculates movement vectors (horizontal vs vertical)
- Automatically places counting line perpendicular to dominant movement
- **Vertical line** for left-right movement
- **Horizontal line** for up-down movement

### 2. Detection & Tracking

```
Frame → YOLOv8 Detection → ByteTrack → Unique IDs → Position History

Confidence threshold: 0.3
Filters: aspect ratio (1.2-5.0), size constraints
Maintains ID consistency across frames

3. Counting Logic
pythonFor each tracked person:
  1. Calculate centroid (x, y)
  2. Determine side relative to line (left/right or top/bottom)
  3. Detect side change = crossing
  4. Classify direction:
     - Left→Right or Top→Bottom = ENTRY
     - Right→Left or Bottom→Top = EXIT
  5. Update counters (prevent double-counting)
4. Visualization

Green boxes = Entered
Red boxes = Exited
Blue boxes = Tracking
Yellow line = Counting boundary
Arrows = Entry/Exit directions
```
