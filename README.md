# Traffic Analytics Vision Pipeline: Sub-Frame Kinematics & Tracking

<video src="https://github.com/user-attachments/assets/754f9fdf-d27f-4694-bafc-438e37d65dcf" width="100%" controls></video>

> An edge-ready computer vision infrastructure for automated vehicle detection, deterministic tracking, and high-precision speed estimation using non-calibrated surveillance feeds.

---

## Product Vision & Context

Speed monitoring is traditionally solved with radar or dedicated physical sensors — hardware-heavy solutions requiring complex installation and maintenance. This project was engineered to prove the viability of a software-only alternative: extracting high-precision traffic analytics from standard, low-cost video feeds using classical computer vision and mathematical interpolation.

Developed at **ISEL (Instituto Superior de Engenharia de Lisboa)**, this system demonstrates that robust architectural design can overcome hardware limitations (such as low framerates) to deliver reliable traffic metrics without relying on heavy deep learning models.

---

## Engineering & Architecture Pipeline

The system is built on a deterministic, lightweight Python/OpenCV pipeline, optimized for performance and accuracy:

1. **Dynamic Background Estimation:** Continuous temporal median filtering to isolate the ambient highway background, adapting to lighting variations without heavy computational overhead.
2. **Spatial Perspective Correction (Homography):** 2D plane calibration mapping pixel coordinates to real-world metric distances, annulling camera lens distortion.
3. **Morphological ROI Extraction:** Adaptive Otsu thresholding coupled with advanced morphological operations (open, close, iterative dilation) to eliminate thermal noise and solidify vehicle bounding boxes.
4. **Deterministic Centroid Tracking:** A custom spatial matching engine that tracks the Euclidean distance of bounding box centroids, maintaining ID integrity even during temporary occlusions or dropped frames.
5. **Sub-Frame Kinematics Engine:** To solve the latency of standard 24 FPS video (~41ms uncertainty per frame), the system uses linear mathematical interpolation. It calculates the exact fractional interval at which a vehicle crosses the virtual control lines, yielding highly accurate km/h speed estimates.

---

## Performance & Analytics

Tested on standard highway surveillance footage, the tracking engine successfully isolated and tracked vehicles through the full measurement zone with stable ID persistence.

**Data Output (Sample Segment):**
* **Total Vehicles Detected:** 12
* **Successful Full-Pass Tracking:** 11

| Kinematic Metric | Recorded Value |
|---|---|
| **Mean Traffic Speed** | 73.55 km/h |
| **Peak Speed Detected** | 99.03 km/h |
| **Minimum Speed** | 54.57 km/h |
| **Standard Deviation** | 15.23 km/h |
| **Mean Transit Time** | 0.3565 s |

*Data extracted automatically via the sub-frame analytics engine and exported to annotated video logs.*

---

## Tech Stack

* **Core Engine:** Python 3, OpenCV
* **Data Processing:** NumPy
* **Prototyping & Visualization:** Matplotlib, Jupyter Notebooks

---

## Authors

Engineered by:
* **Rodrigo Neves** (A51452)
* **Ruben Zhang** (A51388)

*Project developed for the Image Processing and Vision architecture module, Winter 2025/26.*
