# Otsu's Thresholding: Adaptive Image Binarization

---

## Objective

Implementation of **Otsu's Method** for automatic optimal threshold determination in image binarization. This statistical approach separates foreground and background by maximizing **between-class variance**, eliminating manual threshold tuning.

---

## Pipeline Overview

### 1. Image Acquisition
* Load image using OpenCV
* Accepts both grayscale and color images (converts color to grayscale)
* Fallback dummy image if input not found

### 2. Histogram Calculation

$$P(i) = \frac{\text{count of pixels with intensity } i}{\text{total number of pixels}}$$
* 256 bins (0-255 intensity levels)
* Normalized to probability distribution

### 3. Iterative Threshold Evaluation
For each threshold $t$ (0 to 255):
* Split into two classes:
    * $C_1$: pixels $\leq t$
    * $C_2$: pixels $> t$
* Calculate class probabilities:

$$P_1(t) = \sum_{i=0}^t P(i), \quad P_2(t) = \sum_{i=t+1}^{255} P(i)$$
* Compute class means:

$$\mu_1(t) = \frac{1}{P_1} \sum_{i=0}^t i \cdot P(i), \quad \mu_2(t) = \frac{1}{P_2} \sum_{i=t+1}^{255} i \cdot P(i)$$

### 4. Between-Class Variance

$$\sigma_b^2(t) = P_1(t) \cdot P_2(t) \cdot \left( \mu_1(t) - \mu_2(t) \right)^2$$
* Optimal threshold maximizes $\sigma_b^2$

### 5. Binarization
* Pixels $> t \rightarrow 255$ (white)
* Pixels $\leq t \rightarrow 0$ (black)

### 6. Visualization
* Original image
* Histogram with threshold line
* Binarized output

---

## Results

### Sample Image 1
[https://Output_of_sample_image1.png](https://Output_of_sample_image1.png)
* Composite output showing original, histogram, and binarized result

### Sample Image 2
[https://Output_of_sample_image2.png](https://Output_of_sample_image2.png)
* Threshold analysis and binarization output

### Sample Image 3
[https://Output_of_sample_image3.png](https://Output_of_sample_image3.png)
* Foreground/background separation results
