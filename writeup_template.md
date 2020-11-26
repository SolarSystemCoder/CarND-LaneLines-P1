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

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 

    1. images to grayscale
    2. Gaussian smoothing
    3. Canny Edge Detection
    4. region mask
    5. hough transform
    6. cv2 interpolation
    7. write to files

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by 

    1. divided left lane and right lane
    2. using draw_lines()
        - calculated average left lane slop and right lane slop from lines
        - calculated the following from lines
          (x value of top left lane, y value of top left lane), (x value of top right lane, y value of top right lane)
          (x value of bottom left lane, y value of bottom left lane), (x value of bottom right lane, y value of bottom right lane)
        - calculated left lane b in y = a*x + b (a = left lane average slop, x = x of top left lane, y = y of top left lane)
        - calculated right lane b in y = a*x + b (a = right lane average slop, x = x of top right lane, y = y of top right lane )
        - from left lane, y = a*x + b, a and b are known
           -> connected (top left x point, top left y point) and (450, a*450+b)
           -> connected (bottom left x point, bottom left y point) and (100, a*100+b)
        - from right lane, y = a*x + b, a and b are known
           -> connected (top right x point, top right y point) and (500, a*450+b)
           -> connected (bottom right x point, bottom right y point) and (940, a*100+b)

The following is one of the outputs.

---

[//]: # (Image References)
[image1]: ./test_images_output/solidWhiteRight.jpg "output"
---


### 2. Identify potential shortcomings with your current pipeline

This is just an initial stage of the project, so there could be a lot of things to be improved.

I realized my pipeline does not work well for optional challege, and I might need to do fine tune on parameters and masking, and I hardcoded endpoint of x values. If image sizes are changed, then it could create an issue as well.

Also, I am not sure how well the pipeline works at night with no sunlight.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to design parameters tuning. I can have a set of parameter values, and different set of parameters can output the results to different folders.

Another potential improvement could be to refactor draw_lines function, so that duplicated code can be another function 
