---
layout: post
title: "C/C++ Logging Frameworks"
date: 2015-05-26
comments: true
categories: [Cpp,Programming]
---

My goal is to find a lightweight, high-performance logging library for use with C/C++, mostly for robotics control and navigation applications. Ref[1] lists a lot of available C/C++ Logging libraries:

- [Boost::Log](http://www.boost.org/doc/libs/release/libs/log/)
- [EasyLogging++](https://github.com/easylogging/easyloggingpp)
- [g2log](http://www.codeproject.com/Articles/288827/g-log-An-efficient-asynchronous-logger-using-Cplus)
- [g3log](https://github.com/KjellKod/g3log)
- [glog](https://code.google.com/p/google-glog/)
- [Log4cplus](http://sourceforge.net/projects/log4cplus/)
- [Log4cpp](http://log4cpp.sourceforge.net/)
- [Log4cxx](http://logging.apache.org/log4cxx/)
- [Pantheios](http://pantheios.sourceforge.net/)
- [spdlog](https://github.com/gabime/spdlog/)
- [reckless](https://github.com/mattiasflodin/reckless)
- [plog](https://github.com/SergiusTheBest/plog)
- [mini-async-log](https://github.com/RafaGago/mini-async-log)

Boost::Log is well implemented and documented, but it's relatively heavyweight. It also can be more difficult to be adapted for more customized applications, for example an application runs on embedded boards with limited hardware resources. So I rule this option out at the first place.

For rest of the options, they are all free, open-source and lightweight. They can be grouped into two categories: synchronous and asynchronous.

**Synchronous libraries**:

* EasyLogging++ (asynchronous mode is in experimental stages)
* glog
* Log4cplus
* Log4cpp
* Log4cxx
* Pantheios (with default settings)
* plog

**Asynchronous libraries**:

* reckless
* g2log
* g3log
* spdlog (support both)
* mini-asyn-log

Asynchronous libraries use separate threads to handle logs so that it will not block the main application for a long time to wait for the logs written to the disk. Not counting the implementation qualities, asynchronous structure is more suitable for applications that emphasize performance and responsiveness.

Another factor I consider is the activeness of the library development and maintenance. Log4cpp and Pantheios haven't been updated for a few years. Potentially they may start introducing issues while compilers and OSs are evolving. Other projects seem to be still active.

1. reckless library is claimed to be self-contained without external dependency. However, it acquires this feature by including files from boost library.

2. g2log and g3log are two generations of the same library by the same author. According to the project introduction, g3log includes new features while g2log focuses on reliability and compiler supports. "Only well, time tested, features from g3log will make it into g2log."[3]

3. spdlog emphasizes speed, just as indicated by its name. I don't see obvious issues in it and according to the benchmarks it provide, it can be even more efficient than g2log in terms of time needed to log 1,000,000 lines in asynchronous mode.

---------------------- Updated on 11/04/2016 -----------------------

I've been using g3log since the original post of this note. And I've integrated it into a few of my robot simulation projects. So far I'm happy with it.

I'm kind of using this library in a non-conventional way, for most of the time. Instead of logging information of events, I'm logging robot state and control data into the log file. Below shows part of a log file created from a quadrotor control simulation.

```
g3log created log at: Thu Nov 03 17:37:49 2016

0,	DATA,	pos_x, pos_y, pos_z, pos_d_x, pos_d_y, pos_d_z, pos_e_x, pos_e_y, pos_e_z, quat_x, quat_y, quat_z, quat_w, quat_d_x, quat_d_y, quat_d_z, quat_d_w, yaw, yaw_d, vel_x, vel_y, vel_z, vel_d_x, vel_d_y, vel_d_z, vel_e_x, vel_e_y, vel_e_z, acc_d_x, acc_d_y, acc_d_z, jerk_d_x, jerk_d_y, jerk_d_z, omega_d_x, omega_d_y, omega_d_z
362411,	DATA,	-1.800000 , 2.000000 , 0.040250 , -1.800000 , 0.600000 , 0.800000 , 0.000000 , -1.400000 , 0.759750 , -0.000000 , -0.000000 , -0.382683 , 0.923880 , 0.224765 , 0.000000 , 0.000000 , 0.974413 , -0.785398 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 24.351215 , -24.351219 , 0.000000
514384,	DATA,	-1.800089 , 1.999949 , 0.040502 , -1.800000 , 0.600000 , 0.800000 , 0.000000 , -1.399949 , 0.759498 , 0.002312 , -0.003727 , -0.382563 , 0.923919 , 0.227719 , 0.001172 , 0.000000 , 0.973726 , -0.785140 , 0.000000 , -0.008881 , -0.005078 , 0.025192 , 0.000000 , 0.000000 , 0.000000 , 0.008881 , 0.005078 , -0.025192 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.573633 , -0.284140 , 0.000000
694525,	DATA,	-1.801170 , 1.999592 , 0.043710 , -1.800000 , 0.600000 , 0.800000 , 0.000000 , -1.399592 , 0.756290 , 0.035642 , -0.051991 , -0.380457 , 0.922648 , 0.231559 , 0.009868 , 0.000000 , 0.972771 , -0.780588 , 0.000000 , -0.072777 , -0.022960 , 0.203654 , 0.000000 , 0.000000 , 0.000000 , 0.072777 , 0.022960 , -0.203654 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 1.569197 , 0.506085 , 0.000000
871028,	DATA,	-1.802876 , 1.999059 , 0.049349 , -1.800000 , 0.600000 , 0.800000 , 0.002876 , -1.399059 , 0.750651 , 0.085447 , -0.093776 , -0.375101 , 0.918262 , 0.235515 , 0.012104 , 0.000000 , 0.971795 , -0.764907 , 0.000000 , -0.083995 , -0.027585 , 0.332757 , 0.000000 , 0.000000 , 0.000000 , 0.083995 , 0.027585 , -0.332757 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.809954 , -0.320561 , 0.000000
1030266,	DATA,	-1.804119 , 1.998787 , 0.058138 , -1.800000 , 0.600000 , 0.800000 , 0.004119 , -1.398787 , 0.741862 , 0.130342 , -0.076177 , -0.371604 , 0.916034 , 0.242111 , 0.010155 , 0.000000 , 0.970195 , -0.748079 , 0.000000 , -0.067079 , -0.008667 , 0.449114 , 0.000000 , 0.000000 , 0.000000 , 0.067079 , 0.008667 , -0.449114 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.000000 , 0.810381 , -1.153780 , 0.000000
......
```

From this log file I can recover the robot state and plot data that I'm interested in. For example, the plot created from the above log file is shown below:

<center><img src="/img/posts/cpp_logging_plot.png" width="750" /></center>

I did a little modification to the original library code so that it can output the log data in a format that is easier for me to interpret later from Matlab or other programs.

Otherwise I don't get any problem that bothers me from using this logging library. If you have any questions in the implementation details or the performance, you can contact with the author of this library directly. He is very nice and replied to my questions fast.

[Reference]

1. [plog git](https://github.com/SergiusTheBest/plog)
2. [g2log presentation]( https://sites.google.com/site/kjellhedstrom2//g2log-efficient-background-io-processign-with-c11#TOC_the_synchronous)
3. [g3log git](https://github.com/KjellKod/g3log)
