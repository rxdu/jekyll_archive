---
layout: post
title: "Install Java Plugin for Web Browers on Ubuntu"
date: 2014-03-24 22:39:20 -0400
comments: true
categories: [Ubuntu]
---

Java plugin is required to download certificates for WPI wireless. It's often required for other applications. Here is a summary of how to do this on Ubuntu.

1.Install Java Runtime Environment 64bit

```
$ sudo add-apt-repository ppa:webupd8team/java
$ sudo apt-get update
$ sudo apt-get install oracle-java7-installer
```

<!-- more -->

2.Enable Java Plugin for Chrome 64bit

```
sudo mkdir /opt/google/chrome/plugins
cd /opt/google/chrome/plugins
sudo ln -s /usr/lib/jvm/java-7-oracle/jre/lib/amd64/libnpjp2.so
```

3.Enable Java Plugin for Mozilla Firefox 64bit

```
cd /usr/lib/mozilla/plugins
sudo mkdir /usr/lib/mozilla/plugins
sudo ln -s /usr/lib/jvm/java-7-oracle/jre/lib/amd64/libnpjp2.so
```

**Note**:

If you don't want to install JRE in the way mentioned above, make sure you give the right path for the command:
``` 
sudo ln -s /<right-path-of-libnpjp2-so>/libnpjp2.so
```

Reference: 
[How to Enable Oracle Java in Your Web Browsers on Ubuntu Linux](http://m.wikihow.com/Enable-Oracle-Java-in-Your-Web-Browsers-on-Ubuntu-Linux)
