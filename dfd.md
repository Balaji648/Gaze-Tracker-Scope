# Data Flow Diagram (DFD)
```mermaid
flowchart TD

    Camera -->|Captures frames| OpenCV[OpenCV Capture]

    OpenCV -->|Video frames| ScreenSetup[Screen Mapper Setup]
    ScreenSetup -->|Screen corners| FaceMesh[MediaPipe FaceMesh]

    FaceMesh -->|Eye and iris landmarks| EyeTracker[Eye Gaze Estimator]
    FaceMesh -->|Face landmarks| HeadPose[Head Pose Estimator]

    EyeTracker -->|Raw eye gaze XY| GazeFusion[Gaze Fusion]
    HeadPose -->|Head direction| GazeFusion

    GazeFusion -->|Combined gaze| Calibration[Calibration Module]
    Calibration -->|Calibrated gaze| Smoothing[Gaze Smoothing]

    Smoothing -->|Stable gaze| ScreenMapper[Screen Coordinate Mapper]
    ScreenMapper -->|Cursor position| Cursor[Cursor or UI Output]

    ScreenMapper -->|Gaze data| LogFile[(gaze_logs)]
    Smoothing -->|Performance stats| LogFile

    LogFile --> Developer[Developer or Analyst]
