# Computer Vision Fundamentals 👁️

## Overview

A comprehensive exploration of classical computer vision techniques including robust model fitting, feature detection & matching, geometric transformations, and line detection. This project demonstrates foundational CV algorithms before deep learning approaches.

## Problem Statement

Understanding classical computer vision is crucial for ML engineers. These techniques form the backbone of many real-world applications like image stitching, panorama creation, object recognition, and augmented reality.

## Project Structure

This notebook covers 4 major CV techniques:

### 1. RANSAC Regression (Robust Fitting)
### 2. ORB Feature Detection & Matching
### 3. Homography Estimation
### 4. Hough Line Detection

---

## What You'll Learn

### Part 1: RANSAC Regression

**Problem:** Fitting a line to noisy data with outliers

**Solution:** RANSAC (Random Sample Consensus)

**Key Concepts:**
- Random sampling of data points
- Model fitting on samples
- Inlier/outlier classification
- Robust parameter estimation

**Algorithm:**
Randomly sample minimum points
Fit model to sample
Count inliers (points close to model)
Repeat N times
Return model with most inliers
**Output:** Regression line that ignores outliers

**Why It Matters:**
- Handles outliers gracefully
- Used in stereo vision, 3D reconstruction
- Foundation for homography estimation

---

### Part 2: ORB Feature Detection & Matching

**Problem:** Find corresponding points between two images

**Solution:** ORB (Oriented FAST and Rotated BRIEF)

**Key Components:**

**1. Keypoint Detection (FAST)**
- Identifies corner-like regions
- Rotation-invariant
- Scale-invariant

**2. Descriptor Generation (BRIEF)**
- Creates binary descriptors for keypoints
- Efficient comparison
- Rotated for orientation

**Algorithm Steps:**
Load two images (grayscale)
Detect keypoints using ORB
Generate descriptors for each keypoint
Match descriptors between images
Filter matches using RANSAC
Visualize matching points

**Example Output:**
- Image 1: 5000 keypoints detected
- Image 2: 4800 keypoints detected
- Matches found: ~200-500 (depending on scene overlap)

**Why It Matters:**
- Lightweight (good for mobile/embedded)
- Fast and efficient
- Used in object recognition
- Foundation for homography estimation

---

### Part 3: Homography Estimation

**Problem:** Find the geometric transformation between two images

**Solution:** Homography Matrix (3×3 transformation matrix)

**Mathematical Background:**

A homography matrix H transforms points from one plane to another:
[x']   [h11 h12 h13] [x]
[y'] = [h21 h22 h23] [y]
[1 ]   [h31 h32 h33] [1]

**What It Does:**
- Rotation
- Translation
- Scaling
- Perspective transformation
- Skewing

**Algorithm:**
Detect and match features between images
Get corresponding point pairs
Use RANSAC to filter outliers
Solve for 8 parameters of H matrix
Apply H to transform one image to another

**Applications:**
- **Image Stitching:** Create panoramas
- **Document Scanning:** Correct perspective
- **Augmented Reality:** Place virtual objects
- **Camera Calibration:** Estimate camera parameters

**Real-World Example:**
Image 1 (Front view)
↓
H (homography)
↓
Image 2 (Top-down view)

---

### Part 4: Hough Line Detection

**Problem:** Detect straight lines in images

**Solution:** Hough Transform

**Concept:**
Instead of finding lines in image space, transform to parameter space (ρ, θ).

**Algorithm:**
Apply Canny edge detection
For each edge pixel, compute all possible (ρ, θ) pairs
Accumulate votes in Hough space
Find peaks in accumulator
Threshold and extract lines

**Why Hough Transform?**
- Handles incomplete/broken lines
- Robust to noise
- Finds multiple lines simultaneously
- Works even with gaps

**Applications:**
- Lane detection (autonomous vehicles)
- Building/road detection
- Document analysis
- Medical image analysis

---

## Technical Stack

| Technique | Library | Purpose |
|-----------|---------|---------|
| RANSAC | Scikit-learn | Robust fitting |
| ORB Detection | OpenCV | Feature detection |
| Descriptor Matching | OpenCV | Feature matching |
| Homography | OpenCV | Geometric transformation |
| Canny Edges | OpenCV | Edge detection |
| Hough Transform | OpenCV | Line detection |
| Visualization | Matplotlib | Display results |
| Computation | NumPy | Linear algebra |

---

## Installation

```bash
# Clone repository
git clone https://github.com/najeetha-banu/ComputerVision-Techniques.git
cd ComputerVision-Techniques

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

### Run in Google Colab

1. Open `cv.ipynb` in Google Colab
2. Mount Google Drive (if using images from Drive)
3. Execute cells sequentially
4. Upload your own images to test

### Run Locally

```bash
jupyter notebook cv.ipynb
```

### Key Parameters to Experiment

**RANSAC:**
```python
RANSACRegressor(
    min_samples=2,
    max_trials=100,
    residual_threshold=10
)
```

**ORB:**
```python
orb = cv2.ORB_create(
    nfeatures=5000,  # Number of keypoints
    scaleFactor=1.2,
    nlevels=8
)
```

**Hough Lines:**
```python
cv2.HoughLines(
    edges,
    rho=1,           # Pixel distance precision
    theta=np.pi/180, # Angle precision
    threshold=200    # Minimum votes
)
```

---

## Results

### RANSAC Regression
- **Input:** 100 points with outliers
- **Output:** Fitted line ignoring outliers
- **Visual:** Line plotted with inliers (blue) and outliers (red)

### ORB Feature Matching
- **Image 1:** 5000 keypoints
- **Image 2:** 4800 keypoints
- **Matches:** 200-500 correspondence pairs
- **Visual:** Lines connecting matching points

### Homography Estimation
- **Homography Matrix:** 3×3 transformation matrix
- **Example Output:**
[[-2.657  -0.343  345.738]
[ 0.124   1.432  -12.456]
[ 0.001   0.002    1.000]]

### Hough Line Detection
- **Edges Detected:** ~200-500 edge pixels
- **Lines Found:** 5-20 prominent lines
- **Visualization:** Red lines overlaid on original image

---

## Key Learnings

✅ **RANSAC:** Robust fitting with outliers  
✅ **Feature Detection:** Identifying important image regions  
✅ **Feature Matching:** Correspondence between images  
✅ **Homography:** 2D geometric transformation  
✅ **Hough Transform:** Parameter space voting  
✅ **Image Processing:** Edge detection and filtering  
✅ **Computer Vision Pipeline:** End-to-end CV workflow  

---

## Interview Explanation

> "This project demonstrates classical computer vision techniques that form the foundation of modern CV systems. I implemented RANSAC regression to understand robust model fitting in the presence of outliers—a key problem in vision. I used ORB (Oriented FAST and Rotated BRIEF) for efficient feature detection and matching, which helps identify corresponding points between images. I then estimated a homography matrix using RANSAC to find the geometric transformation between two image planes—useful for image stitching and AR applications. Finally, I implemented Hough line detection using the Hough Transform, which votes in parameter space to detect straight lines robustly. These classical techniques are still relevant today for preprocessing, feature extraction, and geometric analysis in computer vision pipelines."

---

## Applications in Production

| Application | Technique Used |
|-------------|-----------------|
| Panorama/Image Stitching | Homography |
| Autonomous Vehicles | Hough (lane detection) |
| Document Scanning | Homography |
| Augmented Reality | Homography |
| 3D Reconstruction | RANSAC + Homography |
| Medical Imaging | Hough (vessel detection) |
| Object Recognition | ORB Features |
| SLAM (Mapping) | Feature Matching |

---

## Future Enhancements

- [ ] Implement advanced feature detectors (SIFT, SURF)
- [ ] 3D reconstruction from homography
- [ ] Real-time video processing
- [ ] Circle detection (Hough Circle Transform)
- [ ] Shape detection beyond lines
- [ ] Deep learning-based feature detection comparison

---

## Author

**Najeetha Banu**
- M.Tech in AI & Decision Sciences, Manipal Institute of Technology
- Interest in Computer Vision and Image Processing
- 10-month internship at SABIC (Data Science)

## Contact

📧 Email: najeetha2002@gmail.com
🔗 LinkedIn: [https://linkedin.com/in/najeetha-banu](https://www.linkedin.com/in/najeetha-banu-37314820a/)
🐙 GitHub: https://github.com/najeetha-banu



*Project completed: June 2025*
