# **Finding Lane Lines on the Road**

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[original]: ./test_images_output/sample_pipeline/1_original.jpg "Original"
[gray]: ./test_images_output/sample_pipeline/2_gray.jpg "Gray"
[blur]: ./test_images_output/sample_pipeline/3_blur.jpg "Blur"
[edges]: ./test_images_output/sample_pipeline/4_edges.jpg "Canny Edges"
[region]: ./test_images_output/sample_pipeline/5_region.jpg "Region of interest"
[line]: ./test_images_output/sample_pipeline/6_line.jpg "Hough Line"
[final]: ./test_images_output/sample_pipeline/7_final.jpg "Final"


---

### Reflection

### 1. Pipeline

My pipeline consists of 7 steps:
1. Convert images to grayscale
2. Apply gaussian smoothing algorithm to reduce noise and image detail to improve processing
3. Detect edges using the Canny detection algorithm
4. Limit the image processing area to the region of interest. The region of interest is hardcoded to include the area in front of the car
5. Apply the Hough Line Transform alogirthm to detect straight lines and identify lanes
6. Draw semi-transparent red lane indicators on top of the image 
7. Save the image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by: 
1. Grouping all lines into left and right lanes based on the slope of each line
2. Calculating weighted average of the slope and intercept for all lines in each group using line length as weight
3. Using the slope and intercept for each lane, calculate (x,y) coordinates for the extrapolated lane, making the line bound by the region of interest

See combine_lane_lines() and line_from_slope_intercept() functions for more details

Pipeline sample:

![alt text][original]
![alt text][gray]
![alt text][blur]
![alt text][edges]
![alt text][region]
![alt text][line]
![alt text][final]


### 2. Shortcomings with the current pipeline

The pipeline assumes a fixed region of interest. This works only on flat roads. If the car were to drive up a steep hill or approach the top of the hill followed by a ravine, the region will either not extend far enough to probe for the lane direction or go over the horizon

The pipeline works with straight lines only. It fails when the car drives along a curved road. 

If any of the lanes are not marked, nothing will be displayed on the screen

### 3. Possible improvements to the pipeline
Dynamically detect the region of interest by looking for a horizon/rate of lane convergence

Instead of assuming straight lines, fit to a curve

If any of the lines are not detected, make an assumption based on the region of interest or extend beyond the region of interest to try and detect other references, such as sidewalks



