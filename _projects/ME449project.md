---
layout: project
title: ME 449 Mobile Manipulation Capstone
date: December 3rd, 2020
image: /800px-Youbot-capstone.png
---

## Overview
In this project, I wrote software in MATLAB that plans a trajectory for the end-effector of the youBot mobile manipulator (a mobile base with four mecanum wheels and a 5R robot arm), performs odometry as the chassis moves, and performs feedback control to drive the youBot to pick up a block at a specified location, carry it to a desired location, and put it down. The code would generate csv files pertaining to the motion of the youBot mobile manipulator, which would then be upload to V-REP, which would be used to visualize the trajectory.

More details can be found in the <a href="https://github.com/chen2156/ME-449-Robotic-Manipulation">Github repository</a>.

Here is a video of the best working model

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="/800px-Youbot-capstone.png">
    <source src="/bestanimation-2020-12-03_18.24.11.mp4" type="video/mp4">
  </video>
</figure>
