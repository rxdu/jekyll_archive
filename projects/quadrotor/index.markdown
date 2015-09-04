---
layout: page
comments: false
sharing: false
footer: true
---

Autonomous Flight Control of a Quadrotor
=====

Unlike conventional helicopter, the quadrotor have 4 rotors and does not require mechanical linkages to vary the rotor blade pitch angle as they spin. The simplicity in mechanical design and the capability of agile maneuver makes quadrotors ideal platform for research in control and motion planning. The goal of project was to help myself get familiar with both the hardware and software of a quadrotor and accumulate basic knowledge for further research on this type of platform.

* The first time I worked on Quadrotor was during my undergraduate study. At that time, I (along with two other teammates) built and assembled the mechanical parts, used the electronics design and control code from the [MikroKopter](http://wiki.mikrokopter.de/en/MikroKopter) open-source project to get a flying quadrotor. In addition, I built another flight control board based on a Freescale S12XEP100 MCU and wrote drivers for this board to collect sensor data and control motors. Complementary filter was used to process IMU data. I implemented a basic flight attitude control algorithm and tried it on the quadrotor (in replace of the MK control board) but the stabilization performance was rather poor.

The Quadrotor based on MK open-source design

<center><img src="/img/projects/02_quadrotor.JPG" width="560" /></center>

Software developed for sensor data processing with C#

<center><img src="/img/projects/02_Sensor_Monitor.JPG" width="560" /></center>

* When I came to WPI for my Masters, I further studied the theories behind the quadrotor. And it was when I started getting a clearer understanding of how to control a quadrotor. I implemented both attitude and position control and applied them in a simulation in Matlab. I also got a chance to get familiar with the Hummingbird quadrotor research platform and tried parts of my code on this platform.

Attitude and Position Control in Matlab Simulation  

<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/GF0DLWTfk3U?list=UUZavD4SDX_YwDwgSEyUDrcQ" frameborder="0" allowfullscreen></iframe>
</center>
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/hz0nLTGGAxQ?list=UUZavD4SDX_YwDwgSEyUDrcQ" frameborder="0" allowfullscreen></iframe>
</center>

Matlab Plot of 8-shape and M-shape Flight Trajectory
<center>
<img src="/img/projects/quad_eight.jpg" width="280" />
<img src="/img/projects/quad_m.jpg" width="280" />
</center>

AscTec Hummingbird Quadrotor

<center><img src="/img/projects/humming_bird.JPG" width="560" /></center>
