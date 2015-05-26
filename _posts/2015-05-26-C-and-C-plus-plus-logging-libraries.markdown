---
layout: post
title: "C/C++ Logging Frameworks"
date: 2015-05-26
comments: true
categories: [[C/C++,Programming]]
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

Asynchronous libraries use separate threads to handle logs so that it will not block the main application for a long time to wait for the logs written to the disk. Not counting the implementation qualities, asynchronous structure is more suitable for applications that emphasize performance and responsiveness.

Another factor I consider is the activeness of the library development and maintenance. Log4cpp and Pantheios haven't been updated for a few years. Potentially they may start introducing issues while compilers and OSs are evolving. Other projects seem to be still active.

Combining the above two factors, it seems the four libraries in the asynchronous category are good candidates. And in their introductions, they all highlight performance, which is desirable.

1. reckless library is claimed to be self-contained without external dependency. However, it acquires this feature by including files from boost library.

2. g2log and g3log are two generations of the same library by the same author. According to the project introduction, g3log includes new features while g2log focuses on reliability and compiler supports. "Only well, time tested, features from g3log will make it into g2log."[3]

3. spdlog emphasize speed, just as indicated by its name. I don't see obvious issues in it and according to the benchmarks it provide, it can be even more efficient than g2log in terms of time needed to log 1,000,000 lines in asynchronous mode.

In conclusion, g2log and spdlog seem to be the best two options for me to do logging. I will try and compare them in more details with actual code.

[Reference]

1. [plog git](https://github.com/SergiusTheBest/plog)
2. [g2log presentation]( https://sites.google.com/site/kjellhedstrom2//g2log-efficient-background-io-processign-with-c11#TOC_the_synchronous)
3. [g3log git](https://github.com/KjellKod/g3log)
