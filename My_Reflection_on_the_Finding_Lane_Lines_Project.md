# My Project for Detecting Road Lane Lines
See my code at [Github](https://github.com/jinglebot/Finding_Lane_Lines)

### The goals of this project are the following:

1. to be able to use the tools we have learned about in the lesson to identify lane lines on the road,
2. to develop a pipeline on a series of individual images that finds and shows lane lines,
3. to later apply the pipeline result to video streams,
4. to be able to produce results that looks roughly like [P1_example.mp4](https://github.com/udacity/CarND-LaneLines-P1/blob/master/examples/P1_example.mp4).
5. to be able to complete a writeup about this project.

### The steps of this project are the following:

1. Use the **Canny Edge Detection** algorithm to identify the lane lines.
- 1. Convert the given test images to *grayscale*.
- 2. Suppress noise and spurious gradients on the grayed images using **Gaussian smoothing/blurring algorithm**.
- 3. Compute the gradients to show edges of the smoothed images.
- 4. Tweak the high and low thresholds to give the best results.
2. Mask the Canny images to show only the **Region of Interest**.
3. Using the **Hough Transform technique**, superimpose the lane lines on the given test images.
- 1. Extract the line segments from the masked Canny images.
- 2. Tweak the values *rho*, *theta*, *threshold*, *minimum line length* and *maximum line gap* to get the best results.
- 3. Average and extrapolate the detected line segments to map out the full extent of the lane lines.
- 4. Draw just one line for the left side of the lane, and one for the right.
4. Test the pipeline on the test images until they look like those in the examples folder. Save in the `test_images_output` file.
5. Test the pipeline on the test videos until they look like those in the examples folder. Save in the `test_videos_output` file.
6. Reflect on your work in a written report.

***

## My Reflection
### 1. Pipeline description

My pipeline consisted of the steps as enumerated above. Here in my reflection, I would like to focus more on the important details like the parameters I used for computing *Canny Edge* and *Hough Transform*. I think I spent too much time tinkering on those values and running the pipeline to see the effect of changing the values. In the end, I decided on the *threshold* values of 50 and 200 for the *Canny Edge* computation and for the *Hough Transform*: a rho of 2, theta of pi / 180, threshold of 100, minimum line length of 100 and maximum line gap of 130.

As for modifying the `draw_lines()` function in the *Hough Transform*, this was the first strategy I tried. First, I solved for the slope of each line in order to separate the left lines from the right. I summed up all the slope values of the lines on the left side and computed for the average. I also placed all the x values in its own list, and the y values in its own. I looked for the longest line(max)  and got its coordinates. I preferred the y values of the endpoints to be at the top and bottom of the *Region of Interest* polygon. And then, I used the average slope and the top and bottom y values in an extrapolation equation to get the endpoints' x values. I then dabbled between using the endpoints' values to draw the lane line or just draw segment extensions from the longest line to my preferred endpoints. And then, I repeated the same steps on the lines on the right side.

It worked actually. But then, it was too long and crude and not really accurate. Then, I found the `np.polyfit()` method from reading the forums and decided to use it instead. Since the function can be used for various degrees of equation, I figured it'll make my `draw_lines()` function flexible and adjustable.

So, this was my next strategy: to use the `polyfit()`. I separated the left and right lines using the slope formula. For the left lines first, I placed all the x values in its own list and the y values in a separate one. I used the `np.polyfit()` to get the coefficients. I then used them on `np.poly1d()` which is like the equation for y as a function x set in the *first degree*. I wanted my lane lines to be centered and separate at the top up to 1/7 of the screen width size and at the bottom, the whole screen width size. And so, since this time, the `poly1d()` function uses x values, I used as my preferred endpoints' x values for the left lane: 3/7 of the screen width at the top  and the left edge of the screen at the bottom. I used the `poly1d()` on the endpoints' x values to solve for the y values. I used the x and y endpoints values to draw the left lane line. I repeated the steps on the lines on the right side. I used 4/7 of the screen width as my preferred endpoint's x value at the top and the right edge of the screen as the endpoint's x value at the bottom. This makes the lane lines balance and centered.

So now, instead of drawing line segments extracted from the *Hough Transform* technique, the `draw_lines()` displayed only two extended lines, one for the lane on the left and one for the lane on the right.
	
My raw test images are:

- [solidWhiteCurve](test_images_output/solidWhiteCurve_raw.jpg)
- [solidWhiteRight](test_images_output/solidWhiteRight_raw.jpg)
- [solidYellowCurve](test_images_output/solidYellowCurve_raw.jpg)
- [solidYellowCurve2](test_images_output/solidYellowCurve2_raw.jpg)
- [solidYellowLeft](test_images_output/solidYellowLeft_raw.jpg)
- [whiteCarLaneSwitch](test_images_output/whiteCarLaneSwitch_raw.jpg)

My raw video sample is this one:
- [solidWhiteRight_raw](test_videos_output/solidWhiteRight_raw.mp4)

After the `draw_lines()` was improved, the resulting test images are:
- [solidWhiteCurve](test_images_output/solidWhiteCurve.jpg)
- [solidWhiteRight](test_images_output/solidWhiteRight.jpg)
- [solidYellowCurve](test_images_output/solidYellowCurve.jpg)
- [solidYellowCurve2](test_images_output/solidYellowCurve2.jpg)
- [solidYellowLeft](test_images_output/solidYellowLeft.jpg)
- [whiteCarLaneSwitch](test_images_output/whiteCarLaneSwitch.jpg)

My improved output videos are:
- [solidYellowLeft](test_videos_output/solidYellowLeft.mp4)

### 2. Potential shortcomings with my current pipeline

One potential shortcoming would be what would happen when the pipeline is applied on roads that are curved. The `polyfit()` function I used is only applicable to first degree equations and the `cv2.line()` statement is limited to lines only.

Another shortcoming could be when the lighting on the roads are not ideal, like at night. The pipeline will have a hard time computing the edges.

This pipeline is limited to roads with lane lines. Therefore, roads with badly drawn lane lines, dirty roads, rain, fog, flood, objects in front of the camera, or anything that the camera would perceive incorrectly as lane lines or limit its capturing ability will affect the result.

And lastly, the *Region of Interest* should be flexible. For very curvy, rough or bumpy roads where the lane lines on the screen would not stay at the bottom, it won't work. I've tried using the pipeline on videos I shot myself and it wouldn't run. Maybe I'm just a lousy cameraman, I have to investigate on that.

### 3. Suggested possible improvements to my pipeline

A possible improvement would be to extend usefulness of the pipeline on curved roads. Another potential improvement could be to be able to use the pipeline on infrared images to detect lane lines at non-ideal conditions. Also, tweaking the *Region of Interest* to follow swerving lane lines on the screen would be a bonus. There are a lot more improvements that involves more than just the lane lines. What if there are no lane lines? What about pedestrians, traffic signs, overtaking, vehicle speed, crashing birds on the windshield, etc. There are still a lot of factors that should be added to simply detecting lane lines. This is just the first project, I know. There are more to come, I'm just too excited!
