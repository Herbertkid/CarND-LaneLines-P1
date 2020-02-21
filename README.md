# **Finding Lane Lines on the Road** 

## Writeup Template



---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report
###overview
As a driver, when we drive our vehicle we usually need to identify lanes of the road. So that to keep the vehicle in the constraints of the lane. And for self driving vehicle is also a important task to detect lane lines.Also very simple Lane Detection pipeline is possible with simple Computer Vision techniques. The project use computer vision techniques to test lane lines detection.

![output sample][./examples/laneLines_thirdPass.jpg]
![Grayscale](./examples/grayscale.jpg)

---

### Reflection



*1.Pipline
My pipeline consisted of 5 steps. 
First, I converted the images to grayscale for edge detection.

Second I used Gaussian Blur withkernel size of 5 to smoothen the image, so that to use Canny Edge Detector which uses the pixel gradient values and filters the image according to the Lower and Higher threshold provided to find out the edges of the lanes.

Third select the region of interest. I use the size of the image to set my region by a polygon of trapeziodal shape focusing on the lower part where the probability of finding lane is more.


Fourth used the Hough Transform to find out the lines in ROI. each line with 4 values (x1,y1,x2,y2).


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first divide the lines into right_lines and left_lines by the slope of each line and distinct  x-axis by middle of the image's x value.
Then sorted the points of each line by x-axis and use the bigest one and smallest one from right_lines and left_lines to calculate the slope. 
After that use the top point and the slope to calculate the bottom point of lines. 


At last draw the lanes on the original Image as shown in the Output Directory.


shown as below:
![output sample](./test_images_output/line-solidWhiteRight.jpg)

video:
![video](./test_videos_output/solodYellowLeft.mp4)
### 2. Shortcomings

For curved lane that Hough Lines based on straight lines don't work well.

Region of Interest assumes that camera stays at same location and lanes are flat. So there is “guess” work or hard coding involved in deciding polygon vertices and thresholds.

In a word, there are many roads which might not be with lane markings where this won’t work.



### 3. Possible improvements

It would be beneficial to use higher degree curve than lines that on curved road.
A possible improvement would be to have dynamic parameters to Canny, Hough functions.
Another potential improvement could be to have a dynamic ROI selector.
