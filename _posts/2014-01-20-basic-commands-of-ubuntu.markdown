---
layout: post
title: "Basic Commands of Ubuntu"
date: 2014-01-20 18:15:40 -0500
comments: true
categories: [Ubuntu,Linux]
---

1. Switch between GUI and virtual console:

	Console: Ctrl+Alt+F2 ((F1), F2, F3, F4, F5, F6)

	There are six virtual consoles. The console on F1 is used for debug and log output, so is best avoided.

    GUI: Ctrl+Alt+F7

    If GUI crashes, it might be possible to fix the problem in virtual consoles.
    
<!-- more -->

2. Basic file operation
    - Get help: 
    ```
    command --help
    ```
    Run a program: type 
    ```
    ./programname
    ```
    - ls: list files
    
    - cp: copy files and folders
    
    - mv: move file or folder
    
    - rm: remove files
    
    - ln: create a link to a file
    ```
    ln -s myfile.doc ~/Desktop/
    ```
    - grep: search through specified file for a word or phrase
    ```
    grep -I wireless myfile.txt
    ```
    - man: view the manual page for specified command
    
    - nano: simple text editor
    
    - umount: unmount attached storage device
    
    - locate: find specified file; relies on a background datebase that is periodically and automatically upated. The database can be manually updated by typing the "sudo updatedb" command.

3. sudo and gksu

    if you run a graphical application from the command-line it's necessary to precede it with *gksu* instead of *sudo*.
    
    Temporarily switching to root: sudo su
    
    Return to ordinary user account: exit or Ctrl+D

4. List and kill processes

    ps: ps or ps aux|grep firefox
    
    kill: kill + PID

5. Zip and upzip

    zip a file: 
    ```
    zip report.zip report.doc
    ```
    zip a folder: 
    ```
    zip -r reports.zip reports
    ```
    upzip a zip: 
    ```
    upzip archive.zip
    ```
    list files in zip: 
    ```
    upzip -l archive.zip
	```
5. Redirection

    ">": redirect to file
    
    ">>": redirect to the bottom of file
```
ls > listing.txt
ls >> listing.txt
```

6. Piping

    pass the output of one command to another
```
    ls|grep report.doc
```
