---
layout: post
title: "Disable Guest Account in Ubuntu"
date: 2014-01-21 22:16:55 -0500
comments: true
categories: Ubuntu
---

Sometimes you may feel annoying to accidentally login to the guest account on you personal computer. But unlike Mac OS, you cannot disable this account directly from "System Settings".

You can get it by following these steps:

1. Open a terminal and enter command:
```
$ gksudo gedit /etc/lightdm/lightdm.conf
```

2. Add one line at the end of the file:
```
$ allow-guest=false
```

3. Now you should see something like this in the file:
```
[SeatDefaults]
greeter-session=unity-greeter
user-session=ubuntu
allow-guest=false
```

4. Save and exit the file. Restart lightdm:
```
$ sudo restart lightdm
```

Reference: http://www.ubuntugeek.com/ubuntu-tiphow-to-disable-guest-account-in-ubuntu-12-04precise.html