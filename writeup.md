**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I used the gaussian blur to blur out the image. Canny function was then used to detect the edges. To filter and look at only the region of interest a simple triangle is used. The triangle bottom edge is same as the image, while the top vertex was at a yoffset of 50 from the center of the image. Houghlines was finally used to identify & highlight the lanes in the image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by forking into 2 branches, one where the slope is +ve & one where the slope in -ve. In both the branches, I went on to find the minimum y & its associated x, similarly maximum y and its associated x was found. Then I went on to find the average +ve slope and average -ve slope. All these were done on the same scan. To extrapolate the line, I noticed that one end y co-ordinate is the image height itself. So maximum ys were fixed up & the associated xs were calculated using the average slopes that was determined. Finally a line for each type of slope , +ve & -ve, was created using the min & max co-ordinates. This was juxtraposed on the image to highlight the lines with the red color. 

Here is a test image that was used.
![solidYellowCurve](test_images/solidYellowCurve.jpg?raw=true "Original Input")
and here is the output after running though the above pipe line.
![solidYellowCurve](test_images_output/solidYellowCurve.png?raw=true "Pipeline Output")

### 2. Identify potential shortcomings with your current pipeline

1. I could see that though most of time in the video the lane detection works fine. There are times when the lines are way off the lane. 
2. I could also see that for the challenging case, the above solution does not work. Whenever you have turing road my solution does not work well at all.


### 3. Suggest possible improvements to your pipeline

1. A better mask for the region of interest than a simple triangle could minimize detection of edges outside the lanes.
2. Extrapolating using a line knowing the average slope & min & max definitely asks for more errors. I am guessing that using some curve fitting techniques would be the better option here.
3. Ignoring erroneous points using heuristics when calculating the average will increase the accuracy of this approach.
4. determing left vs right using just the sign of the slope is also not right. There might be pics when the lanes have same slope and we need better way to determine left from right, possibly some classifying models.