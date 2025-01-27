+++
title = "Digital Image Processing Fundamentals"
date = 2025-01-27
updated = 2025-01-27
description = "The basic glossary and concepts of digital image processing (Short review)."

[taxonomies]
tags = ["image-processing",
        "Review",]
+++

# Overview

## Glossary

- **Bit Depth**: Number of bits used to represent each pixel (e.g., 8-bit = 256
shades of gray).
- **Contrast**: Difference in intensity between light and dark areas of an
image.
- **Intensity**: Brightness of a pixel in an image.
- **Hue**: Color attribute that distinguishes one color from another.
- **Saturation**: Color attribute that describes intensity of color.
- **Luminance**: Brightness of an image.
- **Chrominance**: Color information of an image.

## Color Models

- **Binary**: Single bit representing black or white.
- **Grayscale**: Single channel representing intensity.
- **RGB**: (Red, Green, Blue) Additive color model
- **CMYK**: (Cyan, Magenta, Yellow, Black) Subtractive color model
- **HSV**: (Hue, Saturation, Value) Color model that separates intensity from
color information.
- **YCbCr**: Color model used in video compression. _Y_ represents luminance,
_Cb_ and _Cr_ represent chrominance.

## Image Enhancement
Improves the visual quality of an image.

### Spatial Domain Methods

- Histogram Equalization: Improves contrast by redistributing intensity values.
- Smoothing Filters: Reduces noise (e.g., mean filter, median filter).
- Sharpening Filters: Highlight edges (e.g., Laplacian, Sobel, Prewitt).

### Frequency Domain Methods

- Fourier Transform: Converts image from spatial to frequency domain.
- Low-Pass Filter (LPF): Removes high-frequency noise.
- High-Pass Filter (HPF): Enhances edges and fine details.

## Image Restoration
Removes noise or degradation from an image.

### Noise Models

- Additive Noise: Noise added to image (e.g., Gaussian, salt-and-pepper).
    - Gaussian Noise: Random variation in intensity values.
    - Salt-and-Pepper Noise: Randomly scattered black and white pixels.

- Multiplicative Noise: Noise multiplies image (e.g., speckle).

### Restoration Filters

- Mean Filter: Replaces pixel with average of surrounding pixels.
- Median Filter: Replaces pixel with median of surrounding pixels. Better than
mean filter for salt-and-pepper noise removal (preserves edges).
- Wiener Filter: Removes noise by estimating signal and noise power. Adapts to
local image variations.
- Inverse Filter: Restores image by deconvolving blurred image with point
spread function (PSF).

## Image Segmentation
Divides image into meaningful regions.

### Thresholding
Converts grayscale image to binary image.

- Global Thresholding: Single threshold for entire image. i.e., pixel value
above threshold is considered object, below threshold is background.
- Adaptive Thresholding: Threshold varies based on local image properties.

### Region-Based Segmentation

- Region Growing: Merges pixels with similar properties.
- Split and Merge: Divides image into smaller regions, then merges regions with
similar properties.

### Edge Detection

- Sobel Operator: Detects edges by calculating gradient magnitude.
- Canny Edge Detector: Detects edges by finding local maxima of gradient
magnitude. Steps:
    1. Apply Gaussian filter to smooth image. (Smoothing)
    2. Calculate gradient magnitude and direction.
    3. Apply non-maximum suppression to thin edges.
    4. Apply hysteresis thresholding to detect strong and weak edges. (Edge
       tracking)
- Prewitt Operator: Detects edges by approximating gradient magnitude.
- Laplacian Operator: Detects edges by finding zero crossings.

## Morphological Operations
Modifies image based on shape of objects. Shape-based analysis.

- Erosion: Shrinks objects in binary image. Removes pixels on object
boundaries.
- Dilation: Expands objects in binary image. Adds pixels to object boundaries.
- Opening: Erosion followed by dilation. Removes small objects.
- Closing: Dilation followed by erosion. Fills small holes.

## Image Compression
Reduces size of image data for storage or transmission.

### Lossless Compression
Retains original quality (i.e., PNG, TIFF).

- Run-Length Encoding (RLE): Replaces consecutive pixels with count and value.
- Huffman Coding: Variable-length encoding based on frequency of symbols.

### Lossy Compression
Sacrifices quality for smaller file size (i.e., JPEG).

- Discrete Cosine Transform (DCT): Converts image (spatial data) to frequency
domain.
- Quantization: Reduces precision of DCT coefficients.
- Entropy Encoding: Variable-length encoding based on probability of symbols.

# Recourses

- [Purdue University – Digital Image Processing I](https://engineering.purdue.edu/~bouman/ece637)

- [Stanford University – Digital Image Processing](https://web.stanford.edu/class/ee368/handouts.html)

- [Oregon State University – ECE 468: Digital Image Processing](https://web.engr.oregonstate.edu/~sinisa/courses/OSU/ECE468/ECE468.html)
