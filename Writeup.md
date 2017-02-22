
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_gray]: ./result/grayscale.png "Grayscale"
[image_blur]: ./result/blur_gray.png "Blur"
[image_edges]: ./result/edges.png "Edges"
[image_line]: ./result/line_img.png "line"
[image_region]: ./result/region.png "Region"
[image_output]: ./result/output_img.png "Result Image"
[image_cluster]: ./result/cluster_img.png "Result Image"

---

### Reflection

###1. the pipeline.

My pipeline consisted of 5 steps. All of the those steps writes down a single
function, *def pipline* First, I converted the images to grayscale,
and get the grayscale image as following:

![alt Gray scale Image][image_gray]

Second, use the Gaussian blur to make image smoothly, and the noise point can
be reduced by blur.

![alt Gray Blur Image][image_blur]

And then, use the Canny function to find out the edges in the image.

![alt Canny Image][image_edges]

Then, use the a trapezoid to crop the image, the rest of image is the the region
which we really care about.

![alt Region Image][image_region]

At last, use the Hough line detection function to find out the  straight line in
the image.

![alt Region Image][image_line]

Finally, combine the line image with the origin image, will got the following:

![alt Result Image][image_output]

---

In order to draw a single line on the left and right lanes, I added a new function
*def cluster*.

In this function, I class all lines into two types, named cluster_1 and cluster_2.

First, I compute the k, b for each line, it means I change the line to parameter
space, and using line's k to class them.

the green lines are the cluster_1 and the blue lines are cluster_2 in following
picture.

![alt Cluster Image][image_cluster]

###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be the cropping region would not work when the
car is uphill or downhill, even the road is roughness, car go to another lane.

Another shortcoming could be the hough line detection would got a lot of noise
when there are shadow or guardrail or others big car coming into image.

Also sometime my pipeline cannot got lane line, because the parameter is hard
written in the code, it cannot change at different environment.

###3. Suggest possible improvements to your pipeline

For the shortcomings I and II, maybe we should determent the cropping region dynamically.

Another potential improvement could be to we should using the information that the
lane lines' position cannot change very quickly. we can use the latest lines position
as the input parameter for the current pipeline function.
