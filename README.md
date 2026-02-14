# Parking Spot Detector and Classifier

**Classical computer vision system for parking space detection and occupancy classification using OpenCV - achieving up to 100% accuracy without deep learning through Harris corners, SIFT features, and Hough transforms.**

## 🎯 Overview

This project demonstrates a **resource-efficient parking space detection system** built entirely with classical computer vision techniques - no deep learning required. By leveraging OpenCV's powerful algorithms including Harris Corner Detection, SIFT keypoints, and Hough Line Transforms, the system accurately identifies parking lanes and classifies spaces as occupied or vacant.

**Why Classical CV Over Deep Learning?**
- ✅ **No training data required** - works out of the box
- ✅ **CPU-only processing** - no GPU needed
- ✅ **Low computational cost** - suitable for edge devices
- ✅ **Interpretable results** - every step is explainable
- ✅ **Fast deployment** - no model training phase

**Key Achievements:**
- ✅ Systematic evaluation across 3 difficulty levels (easy, medium, hard)
- ✅ Up to 100% accuracy on structured parking datasets
- ✅ Maintains 68-88% accuracy even under challenging conditions
- ✅ Robust to varying lighting and partial occlusions
- ✅ Complete research paper documenting methodology

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/yourusername/parking-spot-detector-opencv.git
cd parking-spot-detector-opencv

# Install dependencies
pip install -r requirements.txt

# Run the easy dataset example
jupyter notebook easy_parking_detection.ipynb

# Run the medium dataset example
jupyter notebook medium_parking_detection.ipynb
```

### 📥 Hard Dataset Notebook

Due to file size constraints, the hard dataset implementation is hosted on Google Drive:

**[Download Hard Dataset Notebook](https://drive.google.com/file/d/1ryViyaj0clUgxEKjw1cSbFQSDQWhllQ8/view?usp=sharing)**

This notebook contains the implementation and results for the most challenging dataset with heavy occlusions and shadows.

## 📊 Multi-Level Evaluation

### Performance Across Difficulty Levels

| Difficulty | Dataset Characteristics | Accuracy Range | Key Challenges |
|-----------|------------------------|----------------|----------------|
| **Easy** | Clear parking lines, good lighting, minimal occlusion | **82% - 100%** | Occasional shadow interference |
| **Medium** | Varied lighting conditions, some line occlusion | **68% - 89%** | Shadows, faded parking lines |
| **Hard** | Poor line visibility, heavy occlusion, strong shadows | **68% - 88%** | Line detection failures, false positives |

### Detailed Results

**Easy Dataset:**
- Image 1: 82% accuracy
- Image 2: 100% accuracy ✨
- Image 3: 100% accuracy ✨
- Image 4: 100% accuracy ✨

**Medium Dataset:**
- Image 1: 85% accuracy
- Image 2: 68% accuracy
- Image 3: 89% accuracy

**Hard Dataset:**
- Image 1: 87.5% accuracy
- Image 2: 88% accuracy
- Image 3: 68% accuracy

**Overall Average: ~85% accuracy** across all difficulty levels

## 🛠️ Technical Approach

### Complete Pipeline

```
Input Image
    ↓
Preprocessing (Gamma Correction + Gaussian Blur)
    ↓
Canny Edge Detection
    ↓
Morphological Operations (Dilation + Erosion)
    ↓
Hough Line Transform
    ↓
Line Refinement (Skeletonization)
    ↓
Harris Corner Detection
    ↓
ROI Definition (Grouping + Filtering)
    ↓
Parking Space Dimensions Calculation
    ↓
Rectangle Generation
    ↓
SIFT Keypoint Detection (Occupancy Classification)
    ↓
Final Output (Red = Occupied, Green = Vacant)
```

### Core Techniques

#### 1. Preprocessing & Enhancement
- **Gamma Correction**: Adjusts brightness/contrast (γ=1.8)
- **Gaussian Blur**: Reduces high-frequency noise
- **Canny Edge Detection**: Extracts parking lane boundaries
- **Morphological Operations**: Bridges gaps in detected lines

#### 2. Line Detection
- **Hough Line Transform**: Identifies straight parking lane segments
- **Skeletonization**: Reduces line width to single-pixel thickness
- **Dilation & Erosion**: Refines line quality and removes noise

#### 3. ROI Segmentation
- **Harris Corner Detection**: Identifies parking space boundaries
- **Y-Value Grouping**: Organizes corners into parking rows (tolerance: 10px)
- **Noise Filtering**: Removes groups with <3 points
- **Mean Y-Value Alignment**: Ensures horizontal alignment

#### 4. Parking Space Definition
- **Length Calculation**: Perpendicular distance between corner groups
- **Width Calculation**: Median horizontal distance between points
- **Rectangle Generation**: Creates bounding boxes for each space
- **Boundary Validation**: Ensures rectangles stay within limits

#### 5. Occupancy Classification
- **SIFT Feature Detection**: Identifies prominent keypoints in each ROI
- **Classification Logic**: 
  - Keypoints detected → **Red** (Occupied)
  - No keypoints → **Green** (Vacant)

## 💡 Key Algorithms Used

### Harris Corner Detection
```python
corners = cv2.cornerHarris(refined_lines, blockSize=2, ksize=3, k=0.04)
```

### SIFT Keypoint Detection
```python
sift = cv2.SIFT_create()
keypoints = sift.detect(roi, None)
```

### Hough Line Transform
```python
lines = cv2.HoughLinesP(edges, rho=1, theta=np.pi/180, 
                        threshold=50, minLineLength=30, maxLineGap=10)
```

## 🔬 Challenges & Solutions

| Challenge | Problem | Solution |
|-----------|---------|----------|
| **Line Occlusion** | Cars parked over lines | Morphological dilation to connect fragments |
| **Shadow Interference** | Shadows obscure lines | Gamma correction + adaptive thresholding |
| **Faded Lines** | Worn lines have low contrast | Optimized preprocessing pipeline |
| **Ground Noise** | Tire marks create false corners | Multi-stage Y-value grouping |
| **False Positives** | Shadows misclassified as vehicles | SIFT keypoint size thresholding |

## 📈 Experimental Methodology

**Progressive Complexity Testing:**
1. **Easy Level**: Baseline validation with optimal conditions
2. **Medium Level**: Real-world scenarios with varied lighting
3. **Hard Level**: Stress testing with maximum challenges

This multi-level evaluation demonstrates robust scientific methodology and thorough performance analysis.

## 🎯 Classical CV vs Deep Learning

### Classical CV Wins When:
✅ Parking lines are clearly visible  
✅ Structured environment (parking lots)  
✅ Low-resource hardware (embedded systems)  
✅ No training data available  
✅ Interpretability required  
✅ Fast deployment needed  

### Deep Learning Better For:
⚠️ Heavily occluded or missing lines  
⚠️ Extreme lighting variations  
⚠️ Unstructured environments  

## 🚀 Real-World Applications

- **Smart Parking Systems**: Automated space availability
- **Traffic Management**: Real-time occupancy monitoring
- **Smart Cities**: Urban infrastructure integration
- **Parking Guidance**: Direct drivers to available spaces
- **Edge Deployment**: Low-power embedded systems

## 📚 Research Paper

Complete academic paper included: **[parking_detection_paper.pdf](parking_detection_paper.pdf)**

Covers:
- Detailed methodology
- Complete pipeline explanation
- Experimental results
- Performance analysis
- Challenges and limitations

## 📊 Performance Metrics

| Metric | Value |
|--------|-------|
| **Average Accuracy** | 85% |
| **Best Performance** | 100% (Easy dataset) |
| **Processing Time** | 5-15 seconds |
| **Computational Cost** | CPU-only |

## 🔮 Future Enhancements

- [ ] Adaptive gamma correction
- [ ] Multi-view fusion for occluded lines
- [ ] Temporal analysis for video streams
- [ ] Deep learning hybrid for challenging cases
- [ ] Real-time optimization (<1 second)
- [ ] Mobile deployment

## 🎓 Skills Demonstrated

**Computer Vision:**
- ✅ Edge detection techniques
- ✅ Morphological image processing
- ✅ Feature detection (Harris, SIFT)
- ✅ Geometric transformations
- ✅ ROI extraction and analysis

**Research:**
- ✅ Experimental design
- ✅ Systematic evaluation
- ✅ Performance analysis
- ✅ Academic documentation

## 🤝 Contributing

Research project demonstrating classical CV techniques. Suggestions welcome!

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## ✉️ Contact

**Vaibhav Tamta**
- Email: tamtavaibhav.pec@gmail.com

## 📚 References

### Academic Papers
- Harris, C., & Stephens, M. (1988). "A Combined Corner and Edge Detector"
- Lowe, D. G. (2004). "Distinctive Image Features from Scale-Invariant Keypoints"
- Canny, J. (1986). "A Computational Approach to Edge Detection"

### OpenCV Documentation
- [Hough Line Transform](https://docs.opencv.org/3.4/d9/db0/tutorial_hough_lines.html)
- [Harris Corner Detection](https://docs.opencv.org/4.x/dc/d0d/tutorial_py_features_harris.html)
- [SIFT Features](https://docs.opencv.org/4.x/da/df5/tutorial_py_sift_intro.html)

---

<p align="center">
  <i>Classical computer vision for modern smart city applications 🚗</i>
</p>

<p align="center">
  <i>Efficient, interpretable, and deployable without deep learning</i>
</p>
