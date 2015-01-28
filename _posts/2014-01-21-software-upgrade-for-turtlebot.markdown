---
layout: post
title: "Software Upgrade for Turtlebot"
date: 2014-01-21 21:52:23 -0500
comments: true
categories: [ROS, Turtlebot]
---

This article briefly illustrates how to upgrade the software of turtlebot to Ubuntu 12.04 & ROS Groovy from earlier versions. Several issues that may occur during the upgrade are stated as the supplement of official tutorials from ROS wiki. 

<!-- more -->

The ROS wiki page [Robots/TurtleBot/Robot Setup](http://wiki.ros.org/Robots/TurtleBot/Robot%20Setup) is a good reference but it is not always up to date. It uses the system image provided by willow garage, which has integrated most packages required to run turtlebot. What you mainly need to do are just installing Ubuntu with the modified image and then making some small updates. But it's not easy to find sufficient information about that image to make sure it's exactly what you want and it's fully compatible with your netbook. So this tutorial presents how to install the necessary components separately. 

**Install Ubuntu**

You can download the iso image of Ubuntu 12.04 from its [official website](http://www.ubuntu.com/download). Then burn the image to a flash drive or CD to make a bootable media. The installation steps are very straightforward and you mainly need to make some easy choices and click "next". If necessary, you can have a look at this page [Install Ubuntu 12.04.2 LTS](http://www.ubuntu.com/download/desktop/install-desktop-long-term-support).

**Configure Wireless Network of the Netbook**

Now you have a netbook running Ubuntu. To complete the following steps, you need to make the netbook to have access to the Internet. To connect to WPI network (either wireless or wired), you need to get your computer registered and install required certificate files. Definitely it's more convenient to use the wireless network since the robot needs to move around. You can follow this WPI web page to complete the configuration: [link](http://www.wpi.edu/Academics/CCC/Netops/Wireless/Setup/Linux.html).

**Install ROS**

Follow this wiki page [groovy/Installation/Ubuntu](http://www.ros.org/wiki/groovy/Installation/Ubuntu) to finish the installation of ROS groovy. It should be easy to find the latest installation instruction if the link for the old one is invalid.

**Install Turtlebot Packages**

This [Robots/Turtlebot](http://ros.org/wiki/Robots/TurtleBot) page provides well written documents of ROS packages for turtlebot. First follow [Installation](http://ros.org/wiki/turtlebot/Tutorials/groovy/Installation) step by step. The easiest way should be "Install from Debs". On the [Post-Installation Setup](http://ros.org/wiki/turtlebot/Tutorials/groovy/Post-Installation%20Setup) page, you first need to install chrony for clock synchronization. Don't forget to check the section '''Special Cases'''. Probably you need to take care of [Create Base](http://ros.org/wiki/turtlebot/Tutorials/groovy/Create%20Base) and [Netbook Battery Setup](http://ros.org/wiki/turtlebot/Tutorials/groovy/Netbook%20Battery%20Setup). Be careful that the Netbook Battery Setup instruction is not up to date at the time this wiki is written. The robot cannot find battery information of the netbook from "/proc/acpi/battery/BAT1". Instead, use "/sys/class/power_supply/BAT1" and the command changes to:

```
 $export TURTLEBOT_BATTERY=/proc/acpi/battery/BAT1
```

Follow [Workstation Installation](http://ros.org/wiki/turtlebot/Tutorials/groovy/Workstation%20Installation) and [Network Configuration](http://ros.org/wiki/turtlebot/Tutorials/groovy/Network%20Configuration) to make sure your robot can communicate with the work station successfully.

**More Configurations**

Now you can step to the next section of [http://ros.org/wiki/Robots/TurtleBot Robots/Turtlebot]. Work is still not done. When following the [turtlebot\_bringup/Tutorials/groovy/TurtleBot Bringup](http://ros.org/wiki/turtlebot_bringup/Tutorials/groovy/TurtleBot%20Bringup), probably you will get errors when you try to execute roslaunch command:

```
$roslaunch turtlebot_bringup minimal.launch
```

If you get a error message like this:

```
Failed to open port /dev/ttyUSB0.  Please make sure the Create cable is plugged into the computer.
```

It's because you don't have the necessary access permission to the ttyUSB0 device. The solution is to add the user account you're using to the "dialout" group.

```
 $sudo adduser second_user dialout
```

Now you should be able to successfully roslaunch the above launch file. After starting minimal.launch and then turtlebot_dashboard.launch, you should get information of the robot from the dashboard.

**Conclusion**

If you have managed to get through all steps stated above, you're all set for the upgrade. Actually, the above instruction should still be helpful when you're trying to upgrade the software to a newer version in the future. Basically the ideas should stay the same. Just make sure you have the right combination of Ubuntu version and ROS version. You also need to check all relevant packages for the turtlebot and your project have got support to the version of ROS you're trying to use.

