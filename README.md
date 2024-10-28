# -image-convolution-and-Edge-detection-using-sobel-operator

Here's the code that represents all the image processing methods you can do with Python. It uses the libraries, OpenCV and Matplotlib. Below is what you will find in this list,

1. Edge detection using Sobel method.
   The application of Sobel operator generates Sobel images in both  x  and  y  directions.
   Producing 'sobel_x'and 'sobel_y ' with the application of sobel filter in each directions.
- The `sobel_combined` image will combine these to get the edge intensity map.
   It uses `plt.imshow()` to display these images side-by-side.

2. Gaussian Blur:
   It blurs the image with a Gaussian filter to reduce noise.
   `cv2.GaussianBlur(image, (15, 15), 0)` applies the Gaussian kernel of size \(15 \\\\times 15\\\\.
- The sharp and blurred images are provided side by side for comparison.

3. Gabor Filtering:
  This section of the program produces Gabor filters for various angles and frequencies.
  Gabor filters are used in texture and edge detection. These filters attempt to replicate the neurons of the visual cortex. 
  A script that will create the use of the filters using angle (orientation) and wavelengths (frequencies).
- It will be shown as a grid for different values of filter parameters where the change occurs to the output.

4. Laplacian Edge Detection:
   - The Laplacian operator detects edges. These are areas of sudden rapid intensity changes.
   - This code uses the function `cv2.Laplacian()`, then changes the output to an 8-bit unsigned integer.
   - It shows the original image side by side with the edge-detected one.

5. Fourier Transform for Frequency Spectrum: 
   This code computes the Fourier Transform to analyze the frequency elements in the image.
   `np.fft.fftshift(f_transform)` centers the zero frequency component
   The `magnitude_spectrum` is a plot of the frequency components
   Original Image and its frequency spectrum side by side.
This code is used to perform only the Non-Maximum Suppression of edges in an image as part of the overall complex edge detection algorithm; for example, it can follow a Canny Edge Detector. For better clarity here are further details below.

### Key Concepts:

1. Function Non-Maximum Suppression:
   The function `non_max_suppression(img, D)` takes the following arguments
   1. `img` : gradient magnitude of image.
- `D`: the angles in radians, gradient's direction.
  The program creates an empty array of the same size as img to store the thinned edges, Z.
  Transform angle to degrees and convert it to range 0-180.
- **Pixel Loop**: For each pixel, it compares the pixel's intensity with its neighbors in the gradient direction based on the gradient direction. If the current pixel intensity is greater than its neighbors, it retains the intensity; otherwise, it is set to zero.
 
     - Angle Segmentation:
- **0° Angle (horizontal edges)**: Compare the pixel with its left and right neighbors.
        - 45° Angle**: Compare the pixel with its diagonal neighbors, that is, the bottom-left and top-right.
        - 90° Angle (vertical edges)**: Compare the pixel with its top and bottom neighbors.
- **135° Angle**: Compare the pixel with the other diagonal neighbors (top-left and bottom-right).

2. Gaussian Blur:
   The original image is smoothed using a Gaussian Blur to reduce noise and stabilize the gradient computation. Blur size is \\\\(5 \\\\times 5\\\\) with a standard deviation of 1.4.

3. Computing Gradients:
- Gradients `gx` (horizontal) and `gy` (vertical) are calculated using the Sobel operator, which helps in the edge highlighting.
   - The magnitude of the gradient at each pixel is computed by using \\\\( \\\\sqrt{gx^2 + gy^2} \\\\), which gives a measure of edge strength.
   - The angle of the gradient is determined by using `np.arctan2(gy, gx)`.

4. Applying Non-Maximum Suppression:
- The `non_max_suppression` function is applied to the gradient magnitude and angle to thin out the edges, retaining the most prominent edges in each gradient direction.

5. Displaying Results:
   - The original and NMS-processed images are displayed side-by-side using `Matplotlib`, with the NMS output pointing out thinned edges.

### Purpose:
Non-Maximum suppression prevents keeping only the image edges by eliminating the more ambiguous edge responses, thus aiding the edge detection process of any algorithm.                                                                                                     
