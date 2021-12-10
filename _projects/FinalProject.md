---
layout: project
title: Turtlebot3 & Monocular Range Sensing
date: December 10, 2021
image: /20211104_112847.jpg
---

## Overview
During my final fall quarter at Northwestern, I learned about a new machine learning algorithm called the Gaussian Process.  This algorithm essentially allows someone to predict both the result and measure how confident the result the machine predicts.  In the experiment, I attempt to use the Gaussian Process to predict the depth of the robot's surrounding based on the images read in from a raspberry pi camera.  I then send the results to SLAM, which would allow the robot to produce a map of its surrounding environment

More technical details of the project can be found in this <a href="https://github.com/chen2156/MSRFinalProject">Github repository</a>.

The idea behind the Gaussian Process Model was inspired by this <a href="https://ieeexplore.ieee.org/document/4543324">paper</a>.  In order to train the model, I first had to capture images from the raspberry pi camera as well as the corresponding distances from the LIDAR sensor.  I then unwarped and apply PCA to the image to reduce the dimensions of each column of unwarped image.  I then trained the Gaussian Process Model using the reduced image column dataset and their corresponding distances.  I then applied the model to the camera stream coming from the raspberry pi to determine the distance live and send the results to the SLAM node.  In ordered to see the algorithm in action, I modified the turtlebot3 as shown in the picture on the right to be able to capture images of its surrounding and then ran SLAM to compare the resulting maps which were generated.   

Here are some results I got

## Training the Gaussian Model

# Initial Setup

Initial Image Setup

I built up an enclosed space on the floor with obstacles that the turtlebot would want to drive over.  In order to train the robot, I would drive it around the enclosed area until I deemed it captured enough data regarding to the number of images and LIDAR data

Video of robot driving around the obstacle for training
<iframe width="800" height="500" src="https://www.youtube.com/embed/bA4JS41rgfM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  


Fisheye image from raspberry pi camera   
<img src="/compressedFishEye.gif" width="500"> 



Unwarped image   
<img src="/TrainingUnwarpedImage.gif" width="500" height="200">  



After saving the dataset into a folder as well as the corresponding distances into a csv file, I sent the data into the Gaussian Process Model

# Training the model  

Before the images were sent to the Gaussian Process Model, each of the image's column length was first reduced in column length from 420 pixels down to 6 pixels using PCA.  After the images were reduced, they along with the associated observed distance values were sent into the Gaussian Process Model, which would use it to train itself.  Each column had an associated depth value, which was determined from the LIDAR readings.  Each image had 360 columns.

Gaussian Process Model after training on 360 columns (1 image)  
<img src="/1TrainingImage.png" width="500"> 

Gaussian Process Model after training on 720 columns (2 images)  
<img src="/2TrainingImages.png" width="500">  

Gaussian Process Model after training on 1800 columns (5 images)  
<img src="/5TrainingImages.png" width="500">

Gaussian Process Model after training on 3600 columns (10 images)  
<img src="/10TrainingImages.png" width="500">  

From the graphs, it can be shown that the more images the model trains on, the more accurate the Gaussian Process Model is able to predict.  This shows that if there were 600 images, the model theoretically would be pretty robust in predicting depth given the image itself.  

# Testing the model

To test the model, I ran the robot on a different obstacle course to see how well the map generated compares with that generated from the LIDAR and here were some of the results

Initial Setting of the robot  
<img src="/20211208_221904.jpg" width="500">  

# LIDAR Test  
IRL Video  
<iframe width="560" height="315" src="https://www.youtube.com/embed/G9UpRT2PR7s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Video Generating Map  
<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1420">
    <source src="/LidarMapTake3.mp4" type="video/mp4"/>
  </video>
</figure>  

# Gauss Test  
IRL Video  
<iframe width="560" height="315" src="https://www.youtube.com/embed/Dq6NnVD3Cp0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Video Generating Map  
<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1420">
    <source src="/GaussMapTake3.mp4" type="video/mp4"/>
  </video>
</figure>   

# Analysis of Result  

<img src="/lidarmaptake3.png" width="500"><img src="/gaussmaptake3.jpg" width="500">  
The LIDAR map is on the left, and the Gaussian Process map is on the right.  

The maps shown above unfortunately do not show that the Gaussian Process was able to form a map that was able to generate a map that had any cohesive information, let alone similar to what the LIDAR was able to generate.  What I expected in the experiment from the Gaussian Process is a map that I could discern a room from. There were several factors that might explain why the experiment wasn't successful.  One reason being the mount of processing power required to train a Gaussian Process Model.  When training the model, I frequently ran into issue regarding memory, which when it came down to was the implementation of the Gaussian Process training algorithm in scikit-learn.  Since the paper didn't explicitly state how many columns each image had, I assume there would be 360 columns in each image to match the resolution coming from the LIDAR.  This lead to the algorithm in scikit-learn attempting to allocate 174GB of memory for its array, which seems very unreasonable.  If I were to implement this in the future, I would decrease the number of columns in the images to alleviate the memory due to the fact that the paper's implementation use a SICK laser range finder, which doesn't have the same resolution as the LIDAR on the turtlebot3.  Another way I could overcome the memory issue could be using a different library to run the Gaussian Process like the GPy library, or possible run the code in C or C++ to better manage the memory.  Another reason could be the mirror used in the experiment.  Due to access to parts, I was not able to source a mirror that had an optimal focal length to the turtlebot, which might have affected how far the turtlebot3 camera was actually able to see.  In the future, I would like to spend more time determining what the best focal length used that would be able to give the best range for the camera to see and go and possible find it or design the mirror itself.  Another reason could be down to the inefficiencies of the algorithm itself.  Gaussian Process doesn't perform well when it comes to training on images, and there are other machine algorithm out there more suitable to learn images (ex.Convolution Neural Networks).  In the future, I could also try to implement a different machine learning algorithm that is better suited to learning images.










