# Contour-Based Object Detector

A simple Python script using OpenCV for contour-based object detection and bounding box visualization. This project demonstrates fundamental computer vision techniques including grayscale conversion, inverse binary thresholding, contour extraction, and area-based noise filtering.

## Features

* **Path-Safe Image Loading:** Uses `__file__` resolution to reliably locate target images regardless of the terminal's current working directory.
* **Image Preprocessing:** Converts standard BGR images to grayscale and applies inverse binary thresholding (`cv2.THRESH_BINARY_INV`) to isolate foreground subjects from light backgrounds.
* **Contour Extraction & Filtering:** Detects object outlines using `cv2.findContours` and filters out background noise by evaluating contour areas (`cv2.contourArea(cnt) > 200`).
* **Visual Output:** Draws green bounding boxes around detected objects on a preserved color copy of the original image and displays both the final annotated result and the binary threshold mask side-by-side.

## Project Structure

Based on the workspace layout, the project is organized as follows:

```text
OpenCV/
├── data/                       # Additional sample images and videos
├── object detector/
│   ├── image/
│   │   └── birds.png           # Target input image for detection
│   └── object_detector.py      # Main object detection script
├── opencvEnv/                  # Python virtual environment
├── main.py                     # Root workspace script
└── requirements.txt            # Project dependencies
```

## Prerequisites

* **Python 3.x** (Developed with Python 3.13.9)
* **OpenCV** (`opencv-python`)

## Installation

1. **Navigate to the project root directory:**
   ```bash
   cd /path/to/OpenCV
   ```

2. **Activate your virtual environment:**
   * On Linux/macOS:
     ```bash
     source opencvEnv/bin/activate
     ```
   * On Windows:
     ```bash
     opencvEnv\Scripts\activate
     ```

3. **Install the required dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   *(If you do not have `opencv-python` listed in your requirements file, install it directly via `pip install opencv-python`.)*

## Usage

Run the script from anywhere in your terminal:

```bash
python "object detector/object_detector.py"
```

### Controls
* Once executed, two windows will open: **`original with bounding boxes`** and **`thresh`**.
* Press any key (e.g., `Esc` or `Space`) while focused on an image window to close all windows and exit the program cleanly.

## How It Works

1. **Grayscale & Thresholding:** The script converts the loaded image to single-channel grayscale and applies a binary inverse threshold at pixel intensity `127`. Pixels darker than `127` become white (`255`), and lighter pixels become black (`0`).
2. **Finding Contours:** `cv2.findContours` scans the binary threshold mask to retrieve the coordinates of continuous white regions.
3. **Bounding Box Calculation:** For every detected contour with an area greater than `200` square pixels, `cv2.boundingRect` calculates the top-left coordinates `(x1, y1)`, width `w`, and height `h` to draw a bounding rectangle on the original color image.

## Customization

You can easily adapt the script for different images or lighting conditions by modifying the following parameters in `object_detector.py`:

* **Change Target Image:** Update `'birds.png'` in `os.path.join(script_dir, 'image', 'birds.png')` to point to a different file.
* **Adjust Threshold Sensitivity:** Modify the threshold value (`127`) in `cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY_INV)` depending on contrast. Use `cv2.THRESH_BINARY` instead of `cv2.THRESH_BINARY_INV` if detecting light objects on a dark background.
* **Change Minimum Object Size:** Increase or decrease the `200` threshold in `if area > 200:` to ignore larger artifacts or detect smaller objects.
