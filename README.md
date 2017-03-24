# Finding Lane Lines
SDC-ND Project 1

## This is my first project for the **Self-Driving Car Nanodegree Program**.

### The files contained in this repository are:

1. **P1.ipynb** - a *Jupyter* notebook document written in *Python 3.5* with *Matplotlib, Numpy and Open CV* libraries
2. **P1.html** - a HTML version of P1.ipynb for a convenient peek of the codes
3. **My_Reflection_on_the_Finding_Lane_Lines_Project.md** - a *Markdown* write-up about my take on the project, my approach and musings on creating it
4. **README.md** - an *Markdown* overview of the project repository
5. **test_images_output** - folder containing the annotated version of the files from the *test_images* folder

- The following files are in the *test_images_output* folder:

..1. [solidWhiteCurve](test_images_output/solidWhiteCurve_raw.jpg)
..2. [solidWhiteRight]](test_images_output/solidWhiteRight_raw.jpg)
..3. [solidYellowCurve]](test_images_output/solidYellowCurve_raw.jpg)
..4. [solidYellowCurve2]](test_images_output/solidYellowCurve2_raw.jpg)
..5. [solidYellowLeft]](test_images_output/solidYellowLeft_raw.jpg)
..6. [whiteCarLaneSwitch]](test_images_output/whiteCarLaneSwitch_raw.jpg)
..7. [solidWhiteCurve](test_images_output/solidWhiteCurve.jpg)
..8. [solidWhiteRight]](test_images_output/solidWhiteRight.jpg)
..9. [solidYellowCurve]](test_images_output/solidYellowCurve.jpg)
..10. [solidYellowCurve2]](test_images_output/solidYellowCurve2.jpg)
..11. [solidYellowLeft]](test_images_output/solidYellowLeft.jpg)
..12. [whiteCarLaneSwitch]](test_images_output/whiteCarLaneSwitch.jpg)

6. **test_videos_output** - folder containing the annotated version of the files from the *test_videos* folder

- The following files are in the *test_images_output* folder:

..1. [solidWhiteRight_raw](test_videos_output/solidWhiteRight_raw.mp4)
..2. [solidYellowLeft_raw](test_videos_output/solidYellowLeft_raw.mp4)
..3. [solidWhiteRight](test_videos_output/solidWhiteRight.mp4)
..4. [solidYellowLeft](test_videos_output/solidYellowLeft.mp4)


Find my code at [Finding Lane Lines](https://github.com/jinglebot/Finding_Lane_Lines/).
For a quick view of my code, open *P1.html* on you favorite browser. 
To run my code, open *Jupyter Notebook* via the *Anaconda* terminal. The following libraries are required:

* _Matplotlib_
* _Numpy_
* _Open CV_
  
***

## Project Overview 

### This is the first project in the *Nanodegree Program* with the following goals in mind:

1. to be able to use the tools (e.g. Canny Edge Detection, Region of Interest, Hough Transform technique) we have learned about in the lesson to identify lane lines on the road,
2. to develop a pipeline on a series of individual images that finds and shows lane lines,
3. to later apply the pipeline result to video streams,
4. to be able to produce results that looks roughly like [P1_example.mp4](https://github.com/udacity/CarND-LaneLines-P1/blob/master/examples/P1_example.mp4).
5. to be able to complete a writeup about this project.

Thank you for visiting my repo.
