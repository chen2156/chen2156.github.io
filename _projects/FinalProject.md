---
layout: project
title: Turtlebot3 & Monocular Range Sensing
date: December 10, 2021
image: /20211104_112847.jpg
---

## Overview
During my final fall quarter at Northwestern, I learned about a new machine learning algorithm called the Gaussian Process.  This algorithm essentially allows someone to predict both the result and measure how confident the result the machine predicts.  In the experiment, I attempt to use the Gaussian Process to predict the depth of the robot's surrounding based on the images read in from a raspberry pi camera.  I then send the results to SLAM, which would allow the robot to produce a map of its surrounding environment

More technical details of the project can be found in this <a href="https://github.com/chen2156/MSRFinalProject">Github repository</a>.

The idea behind the Gaussian Process Model was inspired by this <a href="https://ieeexplore.ieee.org/document/4543324">paper</a>.  In order to train the model, I first had to capture images from the raspberry pi camera as well as the corresponding distances from the LIDAR sensor.  I then unwarped and apply PCA to the image to reduce the dimensions of each column of unwarped image.  I then trained the Gaussian Process Model using the reduced image column dataset and their corresponding distances.  I then applied the model to the camera stream coming from the raspberry pi to determine the distance live and send the results to the SLAM node   

Here are some results I got

Initial Setup of the environment  
<img src="/robotsetting.jpg" width="200">  






### Topic 1
His nemore audiam consequat ad, no augue choro assueverit mei. Zril offendit tincidunt ne quo. At commodo integre alienum sea, cu vocent fuisset suscipit nam. Eum ex tation omnesque adversarium, mutat autem putant te nam. Id vix facilis complectitur, vis vitae vivendo euripidis ea, fugit eirmod an vix.

### Topic 2
Ad case nemore equidem mea. Duo te iuvaret appetere appellantur, sint scaevola usu cu. Eum ne aeque ridens prompta. At legendos vulputate eos, pro illum iuvaret cu, ludus vituperata usu no.

### Topic 3
Mel magna discere in. Mea ea dicit homero perfecto. Eam nulla facete scribentur in. Vide volutpat laboramus est cu, usu cu impetus dignissim. Ex pro decore impetus. Ius nihil iisque deterruisset an, ex sanctus verterem his. Doming prompta insolens est ut.

### Topic 4
Quod etiam pri ea, habemus electram ea eos, propriae insolens ea qui. Pro no mollis vituperatoribus. Augue quando delicatissimi ex per, vel ea vidisse dolorem eleifend. Has te aliquid senserit, reque soleat sed ea. At bonorum facilisis disputando est, error tantas appetere nec te. Mel in nobis animal.