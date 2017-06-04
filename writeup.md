# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/result-solidWhiteCurve.jpg "solidWhiteCurve"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gussian filter to smoth out noise, the I apply canny edge detection to get edge images. To avoid non lane edges, I applied masking of trapezoid to get interested edge image. Then apply hough lines detection with variable tweeks.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by clustering left and right line points by looking at slope of those lines, then computing the mean m and b of left and right lane points respectively. y = mx + b. I assume left and right lane cross bottom (y max ) and apex (y min of mask). I draw line with calculated m and b for left and right lanes.A correction has been made to avoid two lanes crossing by computing middle point and offset if cross mid point happened

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![solidWhiteRight][test_images/result-solidWhiteRight.jpg]
![solideWhiteCurve][test_images/result-solidWhiteCurve.jpg]
![solidYellowCurve2][test_images/result-solidYellowCurve2.jpg]
![solidYellowCurve][test_images/result-solidYellowCurve.jpg]
![solidYellowLeft][test_images/result-solidYellowLeft.jpg]
![whiteCarLaneSwitch][test_images/result-whiteCarLaneSwitch.jpg]

Videos files can be found in 

![solidWhiteRight][test_videos_output/solidWhiteRight.mp4]
![solidYellowLeft][test_videos_output/solidYellowLeft.mp4]


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when I run pipeline againstcurves, due to the assumption that I assumpe lane always has y = mx + b, which is not the case, it gives poor result in challenge.mp3

Another shortcoming I observed was lack of stablization between frames, lane detection is stateless in my current implementation


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to apply curve fiting to challenge video instead of assume always line. commute loss function of those two ways and apply approperate drawing scheme

Another potential improvement could be memorize previous lanes and apply latest results on top of previous lane detection results to stablize detection result
