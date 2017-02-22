#**Finding Lane Lines on the Road** 

##Naive solution

---

**Finding Lane Lines on the Road**

The goal of this project is:
* Make a pipeline that finds lane lines on the road

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

###1. Algorithm

My pipeline consisted of 5 steps. 
1. I converted the images to grayscale, then 
2. I applied canny to obtained an image that represents the edges of the original grayscale version.
3. Once I obtained the image with the edges I applied hough transform to obtain lines that could potentially represent the road lines. 
4. Next step consisted in filtering the lines by their slope, discarding lines with absolute slope above 0.8 and below 0.4. This is helpfull for example to discard lines close to horizontal that we see in the last video in the examples below.
5. In order to obtain a single line on the left and right for the current lane, I computed the slope for every line and classified them into left and right lines based on their slope (positive and negative respectively). 
6. Once I had the classification I obtained an average slope (m) and axe intercept (b) for left and right, effectively obtained a unique line equation for the left and a unique line equation for the right lines. 
7. Next and last step was to compute the point at which the two lines intercept. Having this point I use it as starting point for both lines and I make them go all the way down to the bottom of the image.

###2. Shortcommings and potential improvements

1. If the car is not well aligned with the lane the left and right notion is lost and the algorithm will fail. The same would happen if theres considerable occlusion from, for example another car.
2. Sometimes there could be very strong lines comming from objects outside the current lane but not too far. There's no filtering to cluster which would be the best line for each side.
3. Sharp turns will not be detected because of the filters applied and the mask that filters out edges. This could be overcommed by perfoming tests over a range of hypothesis of where the road could be located.
4. There's no temporal consistency. Each frame is computed independently and this could be improved using for example a kalman filter.

###3. Examples

<iframe width="560" height="315" src="https://www.youtube.com/embed/S2I5_z0kKNs" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/2gmweqgOWqU" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/iaHEdL_aJRo" frameborder="0" allowfullscreen></iframe>


