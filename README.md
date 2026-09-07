# EX NO :- 9  Implementation of Erosion and Dilation Using OpenCV

## Aim

To write a Python program using OpenCV to implement the morphological operations **Erosion** and **Dilation** on an image and observe their effects on the boundaries and thickness of objects.

The program performs the following operations:

* Creation of a blank image
* Text insertion using OpenCV
* Image Erosion
* Image Dilation

---

## Experiment Details

* **Experiment No.:** 9
* **Experiment Name:** Erosion and Dilation
* **Name:** deepak sudharshan.b
* **Register No.:** 212225230045

---

## Learning Objective

The objectives of this experiment are:

* To understand the concept of morphological image processing.
* To learn how erosion affects foreground objects.
* To learn how dilation affects foreground objects.
* To understand the role of a structuring element or kernel.
* To implement erosion and dilation using OpenCV.
* To compare the effects of erosion and dilation on an image.

---

## Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (`cv2`)
* NumPy
* Matplotlib

---

## Libraries Used

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

### OpenCV

OpenCV is used for:

* Creating and manipulating images
* Adding text to the image
* Performing erosion
* Performing dilation
* Converting images for display

### NumPy

NumPy is used to create the blank image and the structuring element/kernel.

### Matplotlib

Matplotlib is used to display the input, eroded, and dilated images.

---

# Algorithm

### Step 1: Import Required Libraries

Import OpenCV, NumPy, and Matplotlib.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

### Step 2: Create a Blank Image

A blank image of size **500 × 500** with three color channels is created using NumPy.

```python
image = np.zeros((500, 500, 3), dtype=np.uint8)
```

The image is initially filled with zeros, resulting in a black background.

---

### Step 3: Add Text to the Image

The text **"SABARISH"** is added to the blank image using OpenCV's `cv2.putText()` function.

```python
font = cv2.FONT_HERSHEY_SIMPLEX

cv2.putText(
    image,
    'SABARISH',
    (100, 250),
    font,
    1,
    (255, 255, 255),
    2,
    cv2.LINE_AA
)
```

The text is displayed in white on the black background.

The parameters specify:

| Parameter  |                  Value | Description       |
| ---------- | ---------------------: | ----------------- |
| Text       |             `SABARISH` | Text displayed    |
| Position   |           `(100, 250)` | Starting position |
| Font       | `FONT_HERSHEY_SIMPLEX` | Font type         |
| Font scale |                    `1` | Text size         |
| Color      |        `(255,255,255)` | White             |
| Thickness  |                    `2` | Text thickness    |
| Line type  |              `LINE_AA` | Anti-aliased text |

---

### Step 4: Display the Input Image

The original image containing the text is displayed using Matplotlib.

```python
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Input Image with Text")
plt.axis('off')
```

The BGR image is converted to RGB because OpenCV stores color images in BGR format while Matplotlib normally displays RGB images.

---

### Step 5: Create the Structuring Element

A **3 × 3 square kernel** is created using NumPy.

```python
kernel = np.ones((3, 3), np.uint8)
```

The resulting kernel is:

```text
1 1 1
1 1 1
1 1 1
```

This kernel is used for both erosion and dilation.

---

# Step 6: Image Erosion

Erosion is performed using OpenCV's `cv2.erode()` function.

```python
eroded_image = cv2.erode(image, kernel, iterations=1)
```

The erosion operation causes the foreground regions of the image to shrink.

In this experiment, the white characters become thinner because pixels around the boundaries are removed according to the structuring element.

---

### Display the Eroded Image

```python
plt.imshow(cv2.cvtColor(eroded_image, cv2.COLOR_BGR2RGB))
plt.title("Eroded Image")
plt.axis('off')
```

The output displays the effect of erosion on the text.

---

# Step 7: Image Dilation

Dilation is performed using OpenCV's `cv2.dilate()` function.

```python
dilated_image = cv2.dilate(image, kernel, iterations=1)
```

Dilation expands the foreground regions of the image.

In this experiment, the white characters become thicker because pixels are added around the boundaries.

---

### Display the Dilated Image

```python
plt.imshow(cv2.cvtColor(dilated_image, cv2.COLOR_BGR2RGB))
plt.title("Dilated Image")
plt.axis('off')
```

The output displays the effect of dilation on the text.

---

# Complete Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Create a blank image
image = np.zeros((500, 500, 3), dtype=np.uint8)

# Add text on the image using cv2.putText
font = cv2.FONT_HERSHEY_SIMPLEX

cv2.putText(
    image,
    'SABARISH',
    (100, 250),
    font,
    1,
    (255, 255, 255),
    2,
    cv2.LINE_AA
)

# Display the input image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Input Image with Text")
plt.axis('off')

# Create a simple square kernel (3x3)
kernel = np.ones((3, 3), np.uint8)

# Apply erosion (shrinking effect)
eroded_image = cv2.erode(
    image,
    kernel,
    iterations=1
)

# Display the eroded image
plt.imshow(cv2.cvtColor(eroded_image, cv2.COLOR_BGR2RGB))
plt.title("Eroded Image")
plt.axis('off')

# Apply dilation (expanding effect)
dilated_image = cv2.dilate(
    image,
    kernel,
    iterations=1
)

# Display the dilated image
plt.imshow(cv2.cvtColor(dilated_image, cv2.COLOR_BGR2RGB))
plt.title("Dilated Image")
plt.axis('off')
```

---

# Working Principle

The complete morphological processing pipeline is:

```text
Blank Image
     ↓
Add "SABARISH" Text
     ↓
Display Input Image
     ↓
Create 3×3 Kernel
     ↓
 ┌───────────────┐
 ↓               ↓
Erosion       Dilation
 ↓               ↓
Shrink          Expand
 ↓               ↓
Eroded Image   Dilated Image
```

---

# Erosion

Erosion is a morphological operation that reduces the boundaries of foreground objects.

In this experiment:

* A 3×3 kernel is used.
* One iteration is performed.
* The white text becomes thinner.
* The boundaries of the foreground region shrink.

### Formula

Conceptually, erosion keeps a pixel only when the structuring element fits completely within the foreground region.

---

# Dilation

Dilation is a morphological operation that expands the boundaries of foreground objects.

In this experiment:

* A 3×3 kernel is used.
* One iteration is performed.
* The white text becomes thicker.
* The boundaries of the foreground region expand.

### Formula

Conceptually, dilation adds foreground pixels wherever the structuring element overlaps the foreground region.

---

# Comparison

| Operation | Effect on Object        | Effect on Text       |
| --------- | ----------------------- | -------------------- |
| Original  | No morphological change | Normal thickness     |
| Erosion   | Object shrinks          | Text becomes thinner |
| Dilation  | Object expands          | Text becomes thicker |

---

# Expected Output

## Original Image

The program displays a black 500×500 image containing the white text:

**SABARISH**

The title displayed is:

**Input Image with Text**
<img width="476" height="495" alt="image" src="https://github.com/user-attachments/assets/7629b034-7e93-4f65-8dff-ea904e851273" />

---

## Eroded Image

The text is processed using the 3×3 kernel.

Expected effect:

* Character thickness decreases.
* Foreground boundaries shrink.
* Fine parts of the text may become thinner.

The output is titled:

**Eroded Image**
<img width="472" height="500" alt="image" src="https://github.com/user-attachments/assets/fbc51590-5cc8-4355-93f0-7044b0083eb8" />

---

## Dilated Image

The original text is processed using the same 3×3 kernel.

Expected effect:

* Character thickness increases.
* Foreground boundaries expand.
* The white text appears bolder.

The output is titled:

**Dilated Image**
<img width="467" height="502" alt="image" src="https://github.com/user-attachments/assets/50188efe-fd38-4b67-80aa-8ece457989bd" />

---

# Applications

Morphological operations such as erosion and dilation are commonly used in:

* Noise removal
* Object boundary processing
* Character recognition
* Text image processing
* Image segmentation
* Shape analysis
* Object detection
* Medical image processing
* Document image processing

---

# Advantages

### Erosion

* Helps remove small unwanted foreground regions.
* Can separate connected objects.
* Reduces the size of foreground objects.
* Useful for boundary refinement.

### Dilation

* Helps fill small gaps.
* Connects nearby foreground regions.
* Increases the size of foreground objects.
* Useful for strengthening object boundaries.

---

# Limitations

* The output depends on the size and shape of the kernel.
* Excessive erosion can remove important parts of an object.
* Excessive dilation can merge separate objects.
* Different kernel sizes produce different results.
* The experiment uses only one kernel shape and one iteration.

---

# Result

Thus, the morphological operations **Erosion** and **Dilation** were successfully implemented using OpenCV.

A blank image was created using NumPy, the text **"SABARISH"** was added using `cv2.putText()`, and a **3×3 square kernel** was used to perform erosion and dilation. Erosion reduced the thickness of the text, while dilation increased its thickness.

---

## Developed By

**Name:** deepak sudharshan.b

**Register No:** 212225230045
