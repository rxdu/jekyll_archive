---
layout: page
---

<a name="TOP"></a>

<a name="QUAD"></a>

Building a Quadcopter
======

Quadcopters have been very popular in recently a few years. Hobbyists use quadcopters to do various of interesting things such as aerial filming and FPV flight. Research organizations use them a lot as mobile platforms to do research in control, navigation, mapping etc. A quadcopter has a relative simple mechanical structure and doesn't require expensive sensors, processors and other electronic parts. But stabilization of it involves sensor fusion, automatic control and a lot of other theoretical knowledge. Thus building a quadcopter can be an ideal project for people who have learned some theories in dynamic control and want to put them into practice. You can gain both theoretical and practical experience as well as tons of fun by building a flying robot from scratch.

1. System Components
------
* Hardware
    - Inertial measurement unit (IMU)
    - Flight microcontroller
    - A mechanical frame * 1
    - DC brushless motors * 4
    - DSC for brushless motors * 4
* Software
    - Attitude estimation
    - Attitude control
    - Position control
    - Communications

2. IMU Module 
------
An IMU module is used to estimate the attitude of the quadcopter. Instead of using a commercial flight control board which integrates both a microcontroller and accelerometer/gyro sensors, I'm using separate modules for development and testing. The testing hardware used:

* STM32F4 discovery board
* MPU9250 sensor breakout board
* Serial to USB adapter

<img src="/img/quadcopter/imu.jpg" width="367" />


<p align="right"><a href="#TOP">Back To Top</a></p>
