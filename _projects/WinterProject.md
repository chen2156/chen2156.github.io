---
layout: project
title: Turtlebot3 Frontier Explorer and Shape Tracing
date: March 18, 2021
image: /ori-turtlebot3-burger-1997.jpg
---

## Overview

During the Winter quarter, I learned a lot about turtlebot3, especially when it comes to manipulating it on a map.  For this project, I wrote some ROS software that would allow the turtlebot3 to autonomously explore a simulated world in gazebo and visualize what it sees using SLAM in rviz.  Once it is done exploring the map, I then uploaded an image of a convex shape into the program and have the robot trace the edge of the shape onto the map.

More technical details of the project can be found in this <a href="https://github.com/chen2156/MSRWinterProject2021">Github repository</a>.

Here are some videos of the results I got

turtlebot3 autonomously exploring turtlebot3 world

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1500">
    <source src="/EX6frontierExplorerforturtlebot3world.mp4" type="video/mp4"/>
  </video>
</figure>

turtlebot3 autonomously exploring turtlebot3 house

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1500">
    <source src="/EX6frontierExplorerforturtlebot3house.mp4" type="video/mp4"/>
  </video>
</figure>

turtlebot3 tracing a square in the turtlebot3 house map

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1500">
    <source src="/traceSquare.mp4" type="video/mp4"/>
  </video>
</figure>

turtlebot3 tracing a pentagon in the turtlebot3 house map

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1500">
    <source src="/tracePentagon.mp4" type="video/mp4"/>
  </video>
</figure>

turtlebot3 tracing an octagon in the turtlebot3 house map

<figure class="video_container">
  <video controls="true" allowfullscreen="true" poster="" width="1500">
    <source src="/traceOctagon.mp4" type="video/mp4"/>
  </video>
</figure>

