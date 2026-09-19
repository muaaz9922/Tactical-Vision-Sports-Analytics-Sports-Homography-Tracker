# ⚽ Tactical Vision: Sports Analytics & Homography

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![YOLO](https://img.shields.io/badge/YOLO-00FFFF?style=for-the-badge&logo=yolo&logoColor=black)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

A complete sports analytics pipeline designed to extract tactical insights from standard broadcast camera footage. By leveraging object detection, multi-object tracking, and homography transformations, this system maps players and the ball from a dynamic perspective view onto a static, top-down 2D pitch map (radar view) in real-time.

---

## ✨ Key Features

* **Perspective Transformation (Homography):** Calculates a 3x3 transformation matrix using key pitch landmarks to project pixel coordinates from the camera plane to physical pitch coordinates (e.g., meters).
* **Player & Ball Tracking:** Utilizes state-of-the-art object detection (e.g., YOLOv8) coupled with tracking algorithms (e.g., DeepSORT or ByteTrack) to maintain consistent player IDs across frames.
* **Team Clustering:** Automatically groups players into teams based on jersey color extraction and K-Means clustering in the HSV color space.
* **Physical Analytics:** Calculates real-world metrics including player speed, total distance covered, and acceleration by analyzing trajectories on the calibrated top-down map.
* **Tactical Radar View:** Generates a synchronized minimap overlay showing the real-time spatial distribution of both teams and the ball.

---

## 🏗️ Pipeline Architecture

```text
+-----------------------+       +------------------------+
| Broadcast Video Feed  |       | Pitch Calibration Data |
| (Perspective View)    |       | (Reference Points)     |
+-----------+-----------+       +-----------+------------+
            |                               |
            v                               v
+-----------+-----------+       +-----------+------------+
| Object Detection      |       | Homography Matrix (H)  |
| (Players, Ref, Ball)  |       | Calculation            |
+-----------+-----------+       +-----------+------------+
            |                               |
            v                               |
+-----------+-----------+                   |
| Multi-Object Tracking |                   |
| (Assign Track IDs)    |                   |
+-----------+-----------+                   |
            |                               |
            v                               |
+-----------+-----------+                   |
| Team Clustering       |                   |
| (Jersey Color ID)     |                   |
+-----------+-----------+                   |
            |                               |
            +---------------+---------------+
                            |
                            v
                +-----------+-----------+
                | Coordinate Projection | 
                | (Warp to 2D Pitch)    |
                +-----------+-----------+
                            |
                            v
                +-----------+-----------+
                | Analytics Engine      | (Speed, Distance, Heatmaps)
                +-----------+-----------+
                            |
                            v
                +-----------+-----------+
                | Render Output Video   | (With Radar Minimap)
                +-----------------------+
