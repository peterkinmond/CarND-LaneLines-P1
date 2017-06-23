# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image2]: ./test_images_output/gray.jpg
[image3]: ./test_images_output/canny.jpg
[image4]: ./test_images_output/masked_edges.jpg
[image5]: ./test_images_output/whiteCarLaneSwitch.jpg

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:
1. Convert the images to grayscale
![alt text][image2]
2. Use Gaussian smoothing to blur images and reduce noise
3. Use Canny transform to detect edges
![alt text][image3]
4. Limit edges to a specified area in the image
![alt text][image4]
5. Run Hough transform on edges image
6. Overlay lines onto original image
![alt text][image5]



In order to draw a single line on the left and right lanes, I modified the draw_lines() function by iterating through all the lines and figuring out if they belong to the "left" or "right" lane lines by checking the slope angle. For any lines with a positive slope, those belonged to the right lane line. I then used the `np.polyfit` command to find the polynomial fit and then calculated the start and end points for each lane line. For the `y` values, the max y is the total height of the image and the min y is around 50%, which matched nicely with where the lane lines usually appear.


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when an image has lane lines that are outside of the "mask" that I set. It uses some hard-coded values to estimate which area in the images the lane lines will appear in. 

Another potential shortcoming is the thresholds for the Canny transform. They work for the current set of images (sunny, bright, good visibility) but might not work as well for other weather types.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to make the edge mask calculate the area dynamically based on features in the image.
