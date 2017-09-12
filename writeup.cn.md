# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

我的pipeline 包含了

将黄颜色的车道线转成白色。因为黄颜色的线在经过灰度处理后分辨度会降低，转成白色后分辨度能显著提升。

将图片进行灰度处理

使用高斯模糊对图片进行处理

使用 canny 方法识别出图片里的edges

经过观察发现车道线只出现在图片的特定区域中。裁剪出图片中这一特定区域，只识别这个区域的图片，排除其他区域图片的干扰

使用 hough 方法识别直线

计算识别出的直线的斜率，保留斜率在 (0.5 -1) 之间斜率的左车道线和 (-1, -0.5) 之间斜率的右车道线。(这里计算的斜率为y 值经过转换为正常左边轴的斜率), 删除其它噪声线

通过linear regression model 分别拟合保留的左车道线和右车道线，并以指定Y轴为线段起始点算出最终产出的车道线起点终点坐标。

最后将产出的车道线画在图片上

除此之外我还增加了一些debug 的代码，极大得提高了调参的效率

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

这个方案比较依赖参数的选择，在新的场景下可能需要调整参数，普适性不够

方案画的是直线，对于曲率比较大的转弯车道线无法处理

One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

由于目前的算法得出的车道线并不具有robust, 因此可以考虑通过机器学习来建立一个 robust 的方法

在 ZuWhan Kim 2008 年提出的论文 <Robust Lane Detection and Tracking in Challenging Scenarios> 中，作者就提出了用 ANN, SVM 来建立模型识别车导线，取得了良好的效果
A possible improvement would be to ...

Another potential improvement could be to ...


