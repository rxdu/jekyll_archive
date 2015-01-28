---
layout: post
title: "How to fix 'libgazebo_common.so.1 not found' error on Ubuntu 12.04"
date: 2014-01-21 21:36:56 -0500
comments: true
categories: [Ubuntu, Gazebo, ROS]
---

Reference:[Gazebo Answers](http://webcache.googleusercontent.com/search?q=cache:BPYPhX2gWWsJ:answers.gazebosim.org/question/2338/on-ubuntu-1204-libgazebo_commonso1-not-found/+&cd=2&hl=en&ct=clnk&gl=us)

With ROS Groovy installed on Ubuntu 12.04, I was trying to install Gazebo simulator. I followed instructions on this page: http://gazebosim.org/wiki/1.6/install#Compile_Instructions. Following Compile Instructions, gazebo was installed in the default directory, but step 11 gave the error: 

```
$ gazebo
gazebo: error while loading shared libraries: libgazebo_common.so.1: cannot open shared object file: No such file or directory
```
<!-- more -->

From the Gazebo Answers website, I found the solution to this problem provided by *gerkey*. It seemed the original link for this ask-and-answer post was broken and only a cached paged by google could be visited. Since this post solved my problem, I copy it here for future reference:

--------------------------------------------------
Answer:

```
sudo bash -c "echo /usr/local/lib >> /etc/ld.so.conf"
sudo ldconfig
```

First, let's understand the situation:

```
ldd `which gazebo` | grep "not found"
```

That will give you a list of the libraries that the executable needs, but that the loader can't find. Probably libgazebo\_common.so will be in that list, likely along with many other lib\_gazebo\* libraries.

If you did a default install, it went into /usr/local. By default, your system loader might be configured not to look in /usr/local/lib. To test that, add that directory to your LD_LIBRARY_PATH:

```
LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH ldd `which gazebo` | grep "not found"
```

If that gives you an empty list, then you're ready to go, in which case you run gazebo like so:

```
LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH gazebo
```

or:

```
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
gazebo
```

But it's better not to have to remember that. So you can configure your system to look in /usr/local/lib for libraries:

```
sudo bash -c "echo /usr/local/lib >> /etc/ld.so.conf"
sudo ldconfig
```

That should work for gazebo and for anything else that you install to /usr/local.
