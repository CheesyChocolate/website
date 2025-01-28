+++
title = "Digital Image Processing Fundamentals"
date = 2025-01-27
updated = 2025-01-28
description = "The basic glossary and concepts of digital image processing (Short review)."

[taxonomies]
tags = ["image-processing",
        "Review",]

[extra]
toc = false
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

---

# Quiz

## Question 0x01

Approaches to image processing that work directly on the pixels of incoming
image work in ____________.

1. [ ] Spatial domain
2. [ ] Inverse transformation
3. [ ] Transform domain
4. [ ] None of the Mentioned

### Answer 0x01

{{spoiler(fixed_blur=true, text=
"1. Spatial domain. The spatial domain refers to the image plane itself, where
the image is defined by its pixel values."
)}}

## Question 0x02

Which of the following is the primary objective of sharpening of an image?

1. [ ] Decrease the brightness of the image
2. [ ] Increase the brightness of the image
3. [ ] Highlight fine details in the image
4. [ ] Blurring the image

### Answer 0x02

{{spoiler(fixed_blur=true, text=
"3. Sharpening an image aids in highlighting small features in the image or
enhancing details that have become blurred owing to factors such as noise
addition."
)}}

## Question 0x03

Which of the following makes an image difficult to enhance?

1. [ ] Dynamic range of intensity levels
2. [ ] High noise
3. [ ] Narrow range of intensity levels
4. [ ] All the mentioned

### Answer 0x03

{{spoiler(fixed_blur=true, text=
"4. Dynamic range of intensity levels, High noise and Narrow range of intensity
levels make it difficult to enhance an image."
)}}

## Question 0x04

Which of the following is the application of Histogram Equalization?

1. [ ] Blurring
2. [ ] Contrast adjustment
3. [ ] Image enhancement
4. [ ] None of the Mentioned

### Answer 0x04

{{spoiler(fixed_blur=true, text=
"3. Dark images are usually Enhancement using Image enhancement."
)}}

## Question 0x05

What is/are the resultant image of a smoothing filter?

1. [ ] Image with reduced sharp transitions in gray levels
2. [ ] Image with high sharp transitions in gray levels
3. [ ] None of the mentioned
4. [ ] All the mentioned

### Answer 0x05

{{spoiler(fixed_blur=true, text=
"1. Explanation: Smoothing filters reduce noise in random noise, which features
sharp gray level transitions."
)}}

## Question 0x06

___________ is/are the feature(s) of a highpass filtered image.

1. [ ] An overall sharper image
2. [ ] Have less gray-level variation in smooth areas
3. [ ] Emphasized transitional gray-level details
4. [ ] All of the mentioned

### Answer 0x06

{{spoiler(fixed_blur=true, text=
"4. Explanation: A highpass filter reduces the low frequency to reduce
gray-level variance in smooth sections while allowing high frequencies to
emphasize transitional gray-level details for a clearer image."
)}}

## Question 0x07

Which of the following techniques is used for edge detection in images?

1. [ ] Histogram equalization
2. [ ] Fourier transform
3. [ ] Sobel operator
4. [ ] Dilation

### Answer 0x07

{{spoiler(fixed_blur=true, text=
"3. Sobel operator. Histogram equalization is used for contrast enhancement,
Fourier transform is used for frequency domain analysis, and Dilation is used
for morphological operations."
)}}

## Question 0x08

What is the purpose of the Fourier transform in image processing?

1. [ ] To detect edges in an image
2. [ ] To convert an image from the spatial domain to the frequency domain
3. [ ] To compress an image
4. [ ] To apply a filter to an image

### Answer 0x08

{{spoiler(fixed_blur=true, text=
"2. To convert an image from the spatial domain to the frequency domain."
)}}

## Question 0x09

Which of the following is the correct definition of "morphological operations"
in image processing?

1. [ ] Operations based on the pixel values
2. [ ] Operations based on the shape or structure of objects in the image
3. [ ] Operations based on color histograms
4. [ ] Operations based on frequency domain transformations

### Answer 0x09

{{spoiler(fixed_blur=true, text=
"2. Operations based on the shape or structure of objects in the image.
Morphological operations are used to modify the shape of objects in an image
based on their structure."
)}}

## Question 0x0a

In the context of image segmentation, what is thresholding used for?

1. [ ] To segment an image based on pixel intensity
2. [ ] To detect edges
3. [ ] To compress the image
4. [ ] To apply filters to the image

### Answer 0x0a

{{spoiler(fixed_blur=true, text=
"1. To segment an image based on pixel intensity. Thresholding is used to
convert a grayscale image into a binary image by segmenting the image based on
pixel intensity. Sobel, Canny, and Prewitt operators are used for edge
detection. Filters are used for image enhancement and restoration."
)}}

## Question 0x0b

Which of the following techniques can be used for image resizing?

1. [ ] Bilinear interpolation
2. [ ] Sobel edge detection
3. [ ] Fast Fourier Transform
4. [ ] Median filtering

### Answer 0x0b

{{spoiler(fixed_blur=true, text=
"1. Bilinear interpolation. Bilinear interpolation is a method used for image
resizing that calculates new pixel values based on the weighted average of
surrounding pixels. Sobel edge detection is used for edge detection, Fast
Fourier Transform is used for frequency domain analysis, and Median filtering
is used for noise reduction."
)}}

## Question 0x0c

Which of the following algorithms is commonly used for image compression?

1. [ ] Canny edge detector
2. [ ] Run-length encoding
3. [ ] K-means clustering
4. [ ] Gradient descent

### Answer 0x0c

{{spoiler(fixed_blur=true, text=
"2. Run-length encoding. Run-length encoding is a lossless compression
algorithm commonly used for image compression. The Canny edge detector is used
for edge detection, K-means clustering is used for image segmentation, and
Gradient descent is an optimization algorithm."
)}}

## Question 0x0d

Which method is commonly used for removing salt-and-pepper noise from an image?

1. [ ] Gaussian smoothing
2. [ ] Median filtering
3. [ ] Histogram equalization
4. [ ] Edge detection

### Answer 0x0d

{{spoiler(fixed_blur=true, text=
"2. Median filtering. Median filtering is commonly used for removing
salt-and-pepper noise from an image by replacing pixel values with the median
of neighboring pixels. Gaussian smoothing is used for noise reduction and
blurring, Histogram equalization is used for contrast enhancement, and Edge
detection is used for detecting edges in an image."
)}}

## Question 0x0e

What does the term "image thresholding" refer to?

1. [ ] Converting a color image to grayscale
2. [ ] Detecting edges in an image
3. [ ] Converting an image into a binary image based on intensity levels
4. [ ] Enhancing image contrast

### Answer 0x0e

{{spoiler(fixed_blur=true, text=
"3. Converting an image into a binary image based on intensity levels. Image
thresholding is the process of converting a grayscale image into a binary image
by segmenting the image based on intensity levels. Converting a color image to
grayscale is known as color space conversion.
)}}

## Question 0x0f

Which of the following techniques is used to obtain a sharper image by
highlighting high-frequency components?

1. [ ] Low-pass filtering
2. [ ] High-pass filtering
3. [ ] Median filtering
4. [ ] Histogram equalization

### Answer 0x0f

{{spoiler(fixed_blur=true, text=
"2. High-pass filtering. High-pass filtering is used to highlight
high-frequency components in an image, resulting in a sharper image. Low-pass
filtering is used to remove high-frequency noise, Median filtering is used for
noise reduction, and Histogram equalization is used for contrast enhancement."
)}}

## Question 0x10

In which of the following situations is a bilateral filter most useful?

1. [ ] Reducing Gaussian noise
2. [ ] Blurring an image
3. [ ] Preserving edges while smoothing an image
4. [ ] Detecting edges

### Answer 0x10

{{spoiler(fixed_blur=true, text=
"3. Preserving edges while smoothing an image. A bilateral filter is most
useful when you want to smooth an image while preserving edges. It achieves
this by considering both spatial and intensity differences between pixels.
Reducing Gaussian noise is typically done with a Gaussian filter, Even though
bilateral filter uses Gaussian kernel, it is not used for reducing Gaussian
noise."
)}}

## Question 0x11

What is a common application of the Fast Fourier Transform (FFT) in image processing?

1. [ ] Image compression
2. [ ] Edge detection
3. [ ] Frequency domain filtering
4. [ ] Morphological transformation

### Answer 0x11

{{spoiler(fixed_blur=true, text=
"3. Frequency domain filtering. The FFT is commonly used in image processing to
convert an image from the spatial domain to the frequency domain, where
frequency domain filtering can be applied to enhance or suppress specific
frequencies in the image. Image compression, Edge detection, and
Morphological transformation are not direct applications of the FFT."
)}}

## Question 0x12

Which type of noise is best reduced using an adaptive filter?

1. [ ] Gaussian noise
2. [ ] Salt-and-pepper noise
3. [ ] Speckle noise
4. [ ] Periodic noise

### Answer 0x12

{{spoiler(fixed_blur=true, text=
"1. Gaussian noise. Adaptive filters are best suited for reducing Gaussian
noise, which is random and can vary in intensity. Median filters are more
effective for reducing salt-and-pepper noise, and Wiener filters are commonly
used for reducing speckle noise. Periodic noise can be reduced using
frequency-domain filtering techniques."
)}}

## Question 0x13

Which of the following is NOT an image restoration technique?

1. [ ] Inverse filtering
2. [ ] Wiener filtering
3. [ ] Image thresholding
4. [ ] Blind deconvolution

### Answer 0x13

{{spoiler(fixed_blur=true, text=
"3. Image thresholding. Image thresholding is a segmentation technique used to
convert a grayscale image into a binary image based on intensity levels.
Inverse filtering, Wiener filtering, and Blind deconvolution are all image
restoration techniques used to recover the original image from a degraded or
noisy version."
)}}

## Question 0x14

Which of the following transforms is most commonly used for edge detection?

1. [ ] Hough Transform
2. [ ] Discrete Cosine Transform
3. [ ] Wavelet Transform
4. [ ] Laplacian Transform

### Answer 0x14

{{spoiler(fixed_blur=true, text=
"4. Laplacian Transform. The Laplacian transform is commonly used for edge
detection in image processing. The Hough Transform is used for line detection,
the Discrete Cosine Transform is used for image compression, and the Wavelet
Transform is used for multi-resolution analysis."
)}}

## Question 0x15

What is the purpose of a Gaussian filter in image smoothing?

1. [ ] To enhance contrast
2. [ ] To preserve edges while reducing noise
3. [ ] To remove high-frequency components
4. [ ] To segment objects in an image

### Answer 0x15

{{spoiler(fixed_blur=true, text=
"2. To preserve edges while reducing noise. A Gaussian filter is used in image
smoothing to reduce noise while preserving edges. It achieves this by
convolving the image with a Gaussian kernel that reduces high-frequency
components while maintaining the overall structure of the image."
)}}

## Question 0x16

Which of the following is used for noise removal while preserving image details?

1. [ ] High-pass filter
2. [ ] Adaptive filter
3. [ ] Histogram equalization
4. [ ] Erosion

### Answer 0x16

{{spoiler(fixed_blur=true, text=
"2. Adaptive filter. Adaptive filters are used for noise removal while
preserving image details by adjusting the filter coefficients based on the
local image characteristics. High-pass filters are used to enhance edges and
fine details, Histogram equalization is used for contrast enhancement, and
Erosion is a morphological operation used to shrink objects in binary images."
)}}

## Question 0x17

Which of the following methods is most suitable for detecting circular objects in an image?

1. [ ] Sobel edge detection
2. [ ] Hough Transform
3. [ ] Fourier Transform
4. [ ] Laplacian filtering

### Answer 0x17

{{spoiler(fixed_blur=true, text=
"2. Hough Transform. The Hough Transform is most suitable for detecting
circular objects in an image by representing them as points in parameter space.
Sobel edge detection is used for edge detection, Fourier Transform is used for
frequency domain analysis, and Laplacian filtering is used for edge detection."
)}}

## Question 0x18

Which of the following is a common application of morphological operations in
image processing?

1. [ ] Edge detection
2. [ ] Noise reduction
3. [ ] Shape analysis
4. [ ] Color correction

### Answer 0x18

{{spoiler(fixed_blur=true, text=
"3. Shape analysis. Morphological operations are commonly used for shape
analysis in image processing, where they modify the shape of objects based on
their structure. Edge detection is performed using edge detection algorithms,
Noise reduction is achieved using filters, and Color correction is done using
color space transformations."
)}}

---

# Recourses

- [Purdue University – Digital Image Processing I](https://engineering.purdue.edu/~bouman/ece637)

- [Stanford University – Digital Image Processing](https://web.stanford.edu/class/ee368/handouts.html)

- [Oregon State University – ECE 468: Digital Image Processing](https://web.engr.oregonstate.edu/~sinisa/courses/OSU/ECE468/ECE468.html)
