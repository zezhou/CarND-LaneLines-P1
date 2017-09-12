# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[canny]: ./examples/canny.png "canny"
[color_conv]: ./examples/color_conv.png "color conv"
[region_interest]: ./examples/region_interest.png "region_interest"
[slop]: ./examples/slop.png "slop"
[hough]: ./examples/hough.png "hough"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of following steps:

First, I converted the yellow color regions in the image to white color regions, because the yellow color area losses a lot of discriminations when it handled by grayscale. In the contrary, the white color region does not reducing discrimination after grayscale.
![color_conv][color_conv]

Second, I converted the images to grayscale, to prepare for subsequent processing.

Then I used gaussian_blur method to handle image in order to suppress noise and spurious gradients.

Then I used canny function to find out edges in the image.

![canny processing][canny]

Then I used a quadrilateral mask to represent the region I would like to retain and masking everything else out. I used region_of_interest function to do this job and got the edges left in the regions.

![region_interest][region_interest]

Then I used hough_lines function to find out straight lines in these edges.

![hough][hough]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by following steps:
I calculated slopes of these straight linaes, and multiply -1 with slop to convert slop to normal axes slop.
Then I retained lines whose slop between (0.5, 1) as left lane, and retained lines whose slop between (-1, -0.5) as right lane.

![slop][slop]

Then I built a model using linear regression algorithm to fit retained lines. 
The model finally outputed single line on the left and right lanes which started from bottom of image.

At last, I draw the single line on the left and right lanes into raw image as output. 

Besides, I wrote some debug codes, which hugely improved the work efficiency.



### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be that the algorithm may need to re-tune the parameters when it comes to a new scenarios. That means this algorithm is not very robust.

Another shortcoming could be the algorithm may not detect the lane during cornering. The algorithm only designs to handle a straight line, and may make mistake when the lane is curve. 

### 3. Suggest possible improvements to your pipeline

Since the algorithm presenting in this project is not very robust, we should take other algorithms, like statistic machine learning or deep Learning, into consideration, to build a more robust method.
For example, ZuWhan Kim et al. 2008 [1] proposed a method using machine learning algorithms including ANN/SVM to detect lane in realtime, and got an impressive performance. 

### 4. REFERENCES
[1] ZuWhan Kim et al. <Robust Lane Detection and Tracking in Challenging Scenarios> IEEE Transactions on Intelligent Transpoortation Systems, 2008 


