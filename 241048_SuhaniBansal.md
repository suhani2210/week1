# 🧠 Manual Edge Detection in Image Processing

This project implements basic edge detection from scratch using convolution, gradient-based methods, and thresholding techniques. The aim is to understand the edge detection pipeline and manually replicate the steps involved in the Canny algorithm.

---

## 🔹 Sobel Edge Detection

### ✅ Steps:
- Applied Sobel operator in both **X** and **Y** directions.
- Combined the results using **weighted addition** and **gradient magnitude**.

### 🔍 Observations:
- Without preprocessing:
  - Edges were **noisy**, **cluttered**, and **lacked definition**.

---

## 🔹 Gaussian Blur

- Introduced **Gaussian Blur** (kernel size: `(5, 5)`) to smooth the image before edge detection.

### ✨ Effect:
- Suppressed noise and minor gradients.
- Produced **more continuous and natural edges**.

---

## 🔹 Thresholding

After edge detection, **binary thresholding** was applied to convert the gradient image into a binary edge map.

### ⚙ Threshold Experiments:
- `30`: Too noisy; most of the image turned white.
- `50`: ✅ **Best result** — edges were well-defined and broad.
- `100+`: Too thin — several important contours lost.

### ✅ Conclusion:
- Threshold value of **50** gave the most visually pleasing results.

---

## 🔹 Scharr Operator

- Implemented the **Scharr operator** in X and Y directions.
- Combined the results and applied the same thresholding process.

### 🔍 Observations:
- Produced **sharper edges** than Sobel.
- A **higher threshold (100)** resulted in sharper edges.
- A **lower threshold (52)** caused blurred results due to weaker gradients passing through.

---

## 🛠 Manual Canny Edge Detection Pipeline

Implemented the Canny process manually using Sobel gradients, magnitude/direction, non-maximum suppression, and hysteresis.

### 📌 Pipeline Stages:

#### 1. Gaussian Blurring
- Reduced noise and smoothed the image.
- Used a `(5, 5)` Gaussian kernel.

#### 2. Gradient Computation (Sobel)
- Computed **Gx** and **Gy** using Sobel operators.
- Used `ksize = 5` for a balance between detail and noise.

#### 3. Gradient Magnitude and Direction
- Calculated magnitude and direction of edges.
- Normalized magnitude to the `0-255` range.

#### 4. Non-Maximum Suppression (NMS)
- Thinned edges by retaining only local maxima along the gradient direction.
- Gradient direction quantized into: `0°`, `45°`, `90°`, `135°`.

#### 5. Double Thresholding
- Classified pixels as:
  - Strong edges
  - Weak edges
  - Non-edges
- **Thresholds used:**
  - `lowThreshold = 5`
  - `highThreshold = 10`
- Lower thresholds helped retain subtle edges.

#### 6. Edge Tracking by Hysteresis
- Promoted weak pixels to strong if connected (8-connectivity).
- Discarded isolated weak edges.

---

## ✅ Summary

- Manual implementation of edge detection revealed the importance of:
  - Preprocessing (blurring)
  - Gradient calculation
  - Threshold tuning
  - Edge refinement via NMS and hysteresis
- **Manual Canny implementation** provided more flexibility and a deeper understanding of edge detection dynamics.