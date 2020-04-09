# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/pipeline.png "Result of Pipeline"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps:

- First, I converted the images to grayscale.
- Then I blurred the image using GaussianBlur with kernel size of 5, to smoothen the image.
- I applied Canny algorithm to find the edges in the image with recommended threshhold ratio of low:high::1:3.
- Once I got the image with edges from previous step, I decided to mask the region of interest so that I focus only in that part. Due to this step, everything outside of the region is blacked out and we avoid any unnecessary noise in further steps.
- After this, I had to find the lines in the image. So, I used HoughLinesP algorithm to find the lines.
- This was followed by drawing these lines on the image. But it would have drawn multiple smaller lines on right and left lanes.
- Thus, in order to draw a single line on the left and right lanes, I modified the draw_lines() function by finding the slope of lines and based on slope, segregating them in left line coordinates and right lines coordinates.
- Then I used the np.polyfit() method to get the coefficients of these two lines which will be later used to find the x-coordinates of these two lines to extrapolate them.
- To extrapolate the lines from bottom of region of interest (roi) till top of it, I used y-coordinates of bottom and top of roi and found the x-coordinates.
- Then using these coordinates, I drew both the lines on the image.
- Then I superimposed this image with the original one to get the highlighted lines in it.

Here is how the pipeline works: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when I hardcode the region of interest and the lines are out of it's boundary. 

Another shortcoming could be if there are other smaller lines near the actual lines, then how can I handle such scenario to get the expected result.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to tune the parameters of HoughLinesP algorithm, Canny algorithm, and other parameters.

Another potential improvement could be to have adaptive region of interest.
