# Fractal Dimension Analysis

Python code for estimating the fractal dimension of cell images using the **box-counting method**.

## Requirements

* Python 3.10+
* NumPy
* OpenCV
* scikit-image

Install the dependencies with:

```bash
pip install numpy opencv-python scikit-image
```

## Project structure

```text
fractal-dimension/
│
├── data_test/
│   └── example.png
│
├── tools.py
├── main.py
├── requirements.txt
└── README.md
```

## How it works

The analysis follows this pipeline:

```text
Input image
    ↓
Image inversion (Optional)
    ↓
Otsu thresholding
    ↓
Binary image
    ↓
Square image
    ↓
Object extraction
    ↓
20 random rotations
    ↓
Box-counting
    ↓
Mean fractal dimension
```

The box-counting function uses box sizes that are powers of two:

```text
2, 4, 8, 16, ...
```

The final result is the mean fractal dimension calculated from the 20 random rotations.

## Usage

```python
import cv2

from main import calculate_fractal_dimension


image = cv2.imread(
    "data_test/example.png",
    cv2.IMREAD_GRAYSCALE
)

mean_D = calculate_fractal_dimension(image)

print(f"Mean D: {mean_D:.4f}")
```

### Reproducible result

By default, the 20 angles are randomly generated.

If you want to obtain the same result in different executions, use a seed:

```python
mean_D = calculate_fractal_dimension(
    image,
    seed=42
)
```

### Change the number of rotations

```python
mean_D = calculate_fractal_dimension(
    image,
    n_rotations=50
)
```

## Main functions

### `calculate_fractal_dimension()`

Main function. Receives an image and returns the mean fractal dimension.

### `prepare_image()`

Crops the main object and places it in a square image.

### `rotate_image()`

Rotates the image by a given angle.

### `fractal_dimension()`

Calculates the fractal dimension using box counting.

The other functions in `tools.py` perform individual image-processing steps such as dilation, cropping, and padding.

## Notes

The input image should be a grayscale image.

Example:

```python
image = cv2.imread(
    "image.png",
    cv2.IMREAD_GRAYSCALE
)
```

The output is a single `float` representing the mean fractal dimension.

```text
Mean D: 1.5740622824533925
```
