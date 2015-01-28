---
layout: post
title: "Remote Desktop of Ubuntu 12.04"
date: 2014-01-21 22:19:51 -0500
comments: true
categories: [Ubuntu, Raspberry_Pi]
---

Install xRDP package:

```
$sudo apt-get install xrdp
```

If you have problem connecting to the desktop, run:

```
$echo "gnome-session --session=ubuntu-2d" > ~/.xsession
$sudo apt-get install gnome-session-fallback
```
