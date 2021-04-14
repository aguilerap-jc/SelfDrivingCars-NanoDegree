# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### Lane Detection pipeline

#### Image Transformation

##### Grayscale transformation

To be able to detect the lines in the image it will be required to do several transformations on the Image which will allow the extraction of relevant information. 

The first item is to change from RGB colorspace to the grayscale colorspace.

Colorspace transformation Images RGB + Grayscale

[//]: # (Image References)

[image1]: ./images/gray.png "Grayscale"

##### Blur image

With the gray image a gaussian blur effect will be added with a Kernel Size of 5 by 5, this is in order to reduce the noise and reduce the amount of false positives when extracting the edges. 

Gaussian Blur Image

[//]: # (Image References)

[image1]: ./images/blur_gray.png "Gaussian Blur"

##### Edge extraction

With the Blured images will proceed to get the edges by using the Canny Edges transformation with a low threshold of 50 and a high threshold of 150.  

[//]: # (Image References)

[image1]: ./images/edges.png "Edges"

##### Mask of the ROI 

With the extracted edges a mask will be created overlapping in the original RGB image. 
In order to create the mask, is important to define the region of interest (ROI) because there will be much coincidences and we want to discard any information is not on a relevant area. 

This region of interest will be defined by a left bottom area with coordinates 0,539 , right bottom area 900,539 and the apex of the image in the coordinate 475,320. 

[//]: # (Image References)

[image1]: ./images/masked_image.png "Masked Grayscale Image"

Once we have the ROI detected lines its time extend the lines by using the Hough Line transformation to do this transformation it is required to define the following parameters:
* Distance resolution in Pixels of the Hough grid (rho)
* Angular resolution in radians of the Hough grid (theta)
* Minimum number of votes, intersections in the hough grid cell (threshold)
* Minimum number of pixels making a line ( min_line_len )
* Maximum gap in pixels between connectable line segments ( max_line_gap )

[//]: # (Image References)

[image1]: ./images/line_image.png "Line Image"

##### Weighted Image

This extended lines are going to use now to draw the lines to be able to see them properly, but we are only interested in a two main lines the one for each side of the vehicle. Additional lines will be noise from other things. In order to filter the lines the slope is calculated and then we ignore all the ones that have slopes higher than an absolute value of 0.5. 

[//]: # (Image References)

[image1]: ./images/weighted.png "Grayscale"


### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
