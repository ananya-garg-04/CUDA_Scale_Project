# CUDA Scale Project

## Description

The contoru_detection.cu C++ program is a full-featured image-processing pipeline that leverages CUDA for parallel execution. It applies multiple processing steps, including RGB-to-grayscale conversion, Gaussian blurring, Sobel edge detection, non-maximum suppression, and double thresholding to perform edge tracking.

### Libraries and Definitions

* Standard Libraries: Includes standard C++ libraries such as <iostream>, <vector>, <string>, <thread>, and directory handling libraries <dirent.h> and <sys/types.h>.
* CUDA Libraries: Includes <cuda_runtime.h> for CUDA runtime functions.
* OpenCV Library: Includes <opencv2/opencv.hpp> for image reading and writing.

### Constants
* MAX_CONCURRENT_STREAMS: Specifies the upper limit for simultaneous CUDA streams, configured to 4.

### CUDA Kernels
* RGB to Grayscale: Converts the input image to grayscale using weighted RGB values.

* Gaussian Blur: Smooths the grayscale image with a 3×3 Gaussian filter.

* Sobel Edge Detection: Calculates gradient magnitude and direction using the Sobel operator.

* Non-Maximum Suppression: Thins edges by removing non-maximum gradient pixels.

* Double Threshold + Hysteresis: Classifies strong/weak edges and connects valid edges through hysteresis.

### Image Processing Function
#### processImage:
* Receives an input image, output filename, and a CUDA stream.

* Allocates required device buffers.

* Transfers the image to GPU memory.

* Sets up block and grid dimensions for kernel execution.

* Runs the processing kernels in order: grayscale conversion, Gaussian blur, Sobel detection, non-maximum suppression, and double thresholding.

* Copies the final output back to the host and saves it.

* Releases all GPU memory allocations.

### Main Function
#### main:
* Accepts the input and output directory paths as command-line arguments.

* Scans the input directory and loads all image files with .jpg or .jpeg extensions.

* Initializes multiple CUDA streams to enable concurrent execution.

* Processes each image in parallel using the processImage function, distributing the work across the CUDA streams.

* Releases resources by properly destroying all created CUDA streams.

### Building Program
```
mkdir build
cd build
cmake ..
make
```
