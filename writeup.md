# **Finding Lane Lines on the Road** 


### Goals of this project

The goals of this project are the following:

* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection

### 1. Description of the pipeline

My pipeline consisted of 5 steps:

* Step 1. Convert the image to grayscale image in preparation of running Canny edge detection algorithm.
* Step 2. Smooth the image by applying Gaussian Blur algorithm to suppress noise and spurious gradients.
* Step 3. Apply Canny edge detection algorithm
* Step 4. Apply mask to keep results only for the interested region
* Step 5. Apply Hough transform to find out lines from the detected edges in the interested region

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:

1. Hough transform identifies many line segments in the image. Some of these are not related with lane marks. These
   outliers are removed from the line sets. Outliers are identified by their slopes and bottom intersection points.
2. Remaining lines are grouped to those belong to the left lane and those belong to the right lane based on their
   slope values
3. Average slope and average bottom intersection values are computed for both left lane group and right lane group.
4. One line is drawn for each left and right lane based on the average slope and average bottom intersection value. The
   line is drawn from the highes y coordinates to the bottom of the image.


### 2. Potential shortcomings with the current pipeline

1. Outlier detection algorithm based on slope cannot identify spurious lines when their slope is approximately parallel to
   lane markers.
2. Edged detection does not work well when the grayscale gradient is not big enough. For example, yellow lane marker with
   bright asphalt does not have gradient big enough in grayscale.
   

### 3. Possible improvements to the current pipeline

1. If the region that lanes have been identified in the previous frame is known, then the mask can be reduced to only a small
   area. This will greatly improve the effectiveness of the mask filter (Step 4).
2. If we know the color of the lane marker, we can fine tune Canny algorithm. For example, if we know that left lane color is yellow
   and the right lane color is white, then we can apply different parameter values for Canny algorithm.