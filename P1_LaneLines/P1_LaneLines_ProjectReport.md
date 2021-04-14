# **Finding Lane Lines on the Road** 

[//]: # (Image References)

[image1]: ./images/gray.png "Grayscale"

[//]: # (Image References)

[image2]: ./images/blur_gray.png "Gaussian Blur"

[//]: # (Image References)

[image3]: ./images/edges.png "Edges"

[//]: # (Image References)

[image4]: ./images/masked_image.png "Masked Grayscale Image"

[//]: # (Image References)

[image5]: ./images/line_image.png "Line Image"

[//]: # (Image References)

[image6]: ./images/weighted.png "Grayscale"

### 1. Lane Detection pipeline

#### Image Transformation

##### Grayscale transformation

To be able to detect the lines in the image it will be required to do several transformations on the Image which will allow the extraction of relevant information. 

The first item is to change from RGB colorspace to the grayscale colorspace.

Colorspace transformation Images RGB + Grayscale

![alt text][image1]

##### Blur image

With the gray image a gaussian blur effect will be added with a Kernel Size of 5 by 5, this is in order to reduce the noise and reduce the amount of false positives when extracting the edges. 

Gaussian Blur Image

![alt text][image2]

##### Edge extraction

With the Blured images will proceed to get the edges by using the Canny Edges transformation with a low threshold of 50 and a high threshold of 150.  

![alt text][image3]

##### Mask of the ROI 

With the extracted edges a mask will be created overlapping in the original RGB image. 
In order to create the mask, is important to define the region of interest (ROI) because there will be much coincidences and we want to discard any information is not on a relevant area. 

This region of interest will be defined by a left bottom area with coordinates 0,539 , right bottom area 900,539 and the apex of the image in the coordinate 475,320. 

![alt text][image4]

Once we have the ROI detected lines its time extend the lines by using the Hough Line transformation to do this transformation it is required to define the following parameters:
* Distance resolution in Pixels of the Hough grid (rho)
* Angular resolution in radians of the Hough grid (theta)
* Minimum number of votes, intersections in the hough grid cell (threshold)
* Minimum number of pixels making a line ( min_line_len )
* Maximum gap in pixels between connectable line segments ( max_line_gap )

![alt text][image5]

##### Weighted Image

This extended lines are going to use now to draw the lines to be able to see them properly, but we are only interested in a two main lines the one for each side of the vehicle. Additional lines will be noise from other things. In order to filter the lines the slope is calculated and then we ignore all the ones that have slopes higher than an absolute value of 0.5. 

![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline

The current pipeline is highly sensible to light and noise from other things that could be similar to a line, the threshold for the houglines could be easily be mistaken and instead of considering the doted line as our relevant line could take some other thing like a trailer or semi that could be going by at the same time. 

It's also depending highly on the ROI and different lines could cause different effects on the filtering that we are creating.

### 3. Suggest possible improvements to your pipeline

Using other colorspace to process the image could be usefull to reduce the dependency on colors. 

Create a more robust logic on extracting the slope of the lines as well as for detecting the right line, by only considering two instead of tracing any possible line. 
