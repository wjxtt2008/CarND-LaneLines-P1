# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/grayscale_solidWhiteCurve.jpg "Grayscale"
[image2]: ./test_images_output/gaussianblur_solidWhiteCurve.jpg "Gaussian blur"
[image3]: ./test_images_output/edges_solidWhiteCurve.jpg "Canny edges"
[image4]: ./test_images_output/region_solidWhiteCurve.jpg "Crop region"
[image5]: ./test_images_output/result_solidWhiteCurve.jpg "Result"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

First, I converted the images to grayscale, 
![alt text][image1]


then I averaged the grayscale to suppress noise and spurious gradients by gaussian smoothing(gaussian_blur)
![alt text][image2]


The third step is to find the edges based on previos ouput by canny edge algorithm.

![alt text][image3]


Next I applied a region of interest mask to filter out detected line segments in other areas of the image.
![alt text][image4]


Last step is using hough transform to find the lines and draw them on the canvas.
![alt text][image5]


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 3 steps:

1) sepaerate left/right lines by slope, drop horizontal or vertial lines

2) for each group of line calcaute the averaged ceneter and slope

3) take cross points of the middle and the button the image with the right/left line as the endpoints, and draw the each lane accordingly with extended thinkness.



If you'd like to include images to show how the pipeline works, here is how to include an image: 


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there's shadow in within the region of interest as we seenn in the challenge vedio which makes the edges and tress the strogest edges instead of lane mark, and the shadow will be marked as lane lines.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to do color slection after getting the lines, which means select only white and yellow lines.
