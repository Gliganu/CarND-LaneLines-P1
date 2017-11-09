# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

The pipeline consisted of several steps:
1) Convert the initial image to grayscale.
2) Blur the grayscale function using GaussianBlur with a kernel_size of 3.
3) Apply the Canny algorithm on the blurred image in order to detect the edges.
4) Apply a mask on the Region of Interest of the image. The vertices, which form a trapezoid, were selected after a visual inspection of different values and are computed as a percentage of the height and width of the image and not by assigning them hardcoded values
5) Apply the Hough Lines algorithm on the ROI from the Canny image.
6) Draw the lines on the image. 
    In order to construct a filled line from the multiple small lines being outputed by the Hough algorithm, the following steps were performed:
        -based on the slope of each line, they were labeled as being either from the left lane marking or from the right lane marking
        
        -for each marking, merge the list of lines together by computing the weighted averate of the slopes and intercepts
        


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when different lighting conditions affect the drivable area, as it can be observed in the Challenge Video.

Another shortcoming could be the fact that the algorithm works under the assumption that the ROI vertices would be at the same relative coordinates in each image, which is of course a false assumption. The ROI should be determined programatically based on the contents of each image.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to introduce a drivable area detector or a Vanishing Point detector in order to automatically compute the ROI and have a different one for each image.

Another potential improvement in the case of video could be to take into consideration the lines drawn at T-1 when drawing the lines at time T because in this way some adjustment could be made in order to prevent the computed lines to vary too much from frame to frame in a video. 
