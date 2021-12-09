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

I initially set up the robot such that it was on a table surrounded by a couple of objects.  I then captured data using ROS, which were the images streaming from the raspberry pi camera and the LIDAR distances generated 

<img src="/frame0000.jpg" width="500">  

Fisheye image from raspberry pi camera   
<img src="/robotSetting.jpg" width="500">   

Unwarped image   
<img src="/frame0000Unwarped.jpg" width="500">  

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

From the graphs, it can be shown that the more images the model trains on, the more accurate the Gaussian Process Model is able to predict.  This proves that if there were 600 images, the model theoretically would be pretty robust in predicting depth given the image itself.  

# Videos driving the turtlebot around

To test the model, I built a robot that performed SLAM while driving around an enclosed space.  The robot was driven around using WASD keys, and corresponding pictures and videos are shown below.

Initial Setting of the robot
<img src="/robotSetting" width="500">  

Robot running with LIDAR







