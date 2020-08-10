# **Finding Lane Lines on the Road** 

The goal of this project is to identify and highlight lane lines on the road.

---

![Input Image](./Images/solidWhiteRight.jpg)
Example Input Image

![Output Image](./Images/laneLines_thirdPass.jpg)
Example with lane lines extrapolated and overlayed

---

## Lane Finding Pipeline
Below is an outline of steps used to create lane lines.

### 1. Convert the image to grayscale
Uses grayscale() function to convert image to grayscale.

### 2. Apply Gaussian Blur to grayscale image
Using the gaussian_blur() function the cv2.GauassianBlur function was applied to grayscale image.

### 3. Identify edges with Canny
Uses the cv2.Canny() function to identify edges in the image.

### 4. Identify a Region of Interest
Uses coordinates in the image to create a polygon Region of Interest. Then uses cv2.fillPoly() function to mask (blackout) pixels outside the region.

### 5. Apply a Hough Transformation to highlight lines identified in the Region of Interest
Uses cv2.HoughLines() function to highlight lines within the region red. Then the draw_lines() function averages and extrapolates these smaller lines into one larger red line.

### 6. Return the weighted image with lane line highlights overlayed with original image
Uses cv2.addWeighted() function to overlay the created red lines with the original image

## Testing on Video
Once the above pipeline worked for static images the next test would be to see how it handles videos. 
![Solid White Line GIF](./Images/solidWhiteRight.gif)
![Solid Yellow Line GIF](./Images/solidYellowLeft.gif)

## Next Steps
The biggest obstacle was creating lane lines that compensated for sharp turns in the road. To overcome these  obstacles there are two methods I would explore next:

1. Instead of relying on the slope of the Canny lines, I could identify two regions (one for the left side lane lines and one for the right). Then I could average slopes of the lines on each side separately .
2. Alternately I could identify the starting and stopping coordinates of each line in the Hough Transformation and create a 'best fit' line through these. It may return some errors near the horizon line, but that can also be compensated by reducing the size of the Region of Interest.
