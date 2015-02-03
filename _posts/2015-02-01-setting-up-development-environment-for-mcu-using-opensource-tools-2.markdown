---
layout: post
title: "Setting Up Development Environment for MCUs with Open-Source Tools (2)"
date: 2015-02-01
comments: true
categories: [Embedded_Development]
---

As introduced in part one, you should have source files, startup code and a linker script at hand first, then compile, assemble, link them to get an executable file, and finally convert the executable file to a binary file that your MCU can understand. In this part, I will explain how to do all these work in detail. I keep figure 1 from the first part of this article for easy reference. 

<center><img src="/img/posts/gnu_toolchain.jpg" width="750" /></center>
<center>Figure 1 Workflow of Cortex-M MCU Development</center>

STM32F4 Discovery board is used as an example platform. But the instructions should work with all Cortex-M based microcontrollers. Moreover, the steps should be very similar for other types of MCUs such as AVRs. Here is a list of the tools that will be used:

1. [GNU Tools for ARM Embedded Processors](https://launchpad.net/gcc-arm-embedded)
2. [Eclipse CDT](https://eclipse.org/cdt/downloads.php)
3. ([GNU ARM Eclipse Plug-ins](http://gnuarmeclipse.livius.net/blog/))

**(1)**The GNU tools for ARM includes all programs (gcc, as, ld, objcopy) that are necessary to build the binary file, in a command line window or Linux terminal. This set of tools and a text editor are the minimal requirements for your development work. Search in Google to find the toolchain for your MCU, for example [AVR 8-bit GNU Toolchain - Linux](http://www.atmel.com/tools/ATMELAVRTOOLCHAINFORLINUX.aspx),[AVR 8-bit GNU Toolchain - Windows](http://www.atmel.com/tools/ATMELAVRTOOLCHAINFORWINDOWS.aspx), [GNU for PIC](http://gputils.sourceforge.net/) and [GNU for HCS12](http://gcc-hcs12.com/) **(2)**Eclipse is an IDE that can be used for programming in many languages. In addition it's free, cross-platform and well supported by a large open-source community. Using Eclipse can make it easier to manage project files and invoke the tools with proper configurations using a graphic user interface. **(3)**The GNU ARM Eclipse Plug-ins can make this configuration process even easier. You can create a project like that in MDK-ARM and IAR. By selecting the model or the family of your microcontroller, the plug-in will set up almost everything for you. But this kind of plug-in is not available for all MCUs. The plug-ins for ARM are well supported currently. But as far as I know the [Eclipse plug-in for AVR](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) is quite out-dated and doesn't work well with the latest version of Eclipse.

---------------

* Install GNU tools

Download the right pre-built gnu toolchain for your operating system. You can find instructions about the installation in the [readme](https://launchpadlibrarian.net/192227680/readme.txt) file if you don't how to do it.

* Install Eclipse CDT

In Windows, you just need to unzip the archived file to a place you like. In Ubuntu, I put the extracted folder to "/opt/eclipse". Of course you're free to put it anywhere else. If you installed a normal Eclipse which is just for Java, remember to install the CDT plugin for C/C++ support.

* Launch Eclipse CDT and create a new C project

Click "File"-"New"-"C Project". Select an "Empty Project" under "Executable" tab, choose "Cross GCC" as the "Toolchains". Give a name to your project. Click "Next" until you see the "Cross GCC Command" page, In "Cross compiler prefix" area, type "arm-none-eabi-". If you're not sure about the prefix, check the "bin" folder in your GNU tool installation directory. In "Cross compiler path", browse to get the location of the "bin" folder of your GNU tool chain installation. Now you have a C project in Eclipse. You can copy your source file into the project. Before successfully compiling the project, you still need to do a few more configurations. 

<center><img src="/img/posts/eclipse_gcc.png" width="650" /></center>
<center>Figure 2 An Example "Cross GCC Command" Page Setup</center>

* Configure project properties

Right click on the project name and open "Properties". Go to "C/C++ Build"-"Settings". Most settings are done here. Configurations under "Tool Settings" tab are for the compiling, assembling and linking. If everything is good, you should be able to get the executable file. This part can be confusing if you have no idea about the GNU toolchain. One thing that's worthy of mentioning is that "gcc" here doesn't just mean the "C Compiler, instead it means the "**G**NU **C**ompiler **C**ollection". This command "gcc" can also invoke the linker and assembler. If you just want to compile without assembling and linking, use "-S" option. Use "gcc --help" for information of all options. Read the "[readme](https://launchpadlibrarian.net/192227680/readme.txt)" file for the most important options you need to specify when invoking gcc. Check the list of [GCC Submodel Options](https://gcc.gnu.org/onlinedocs/gcc/Submodel-Options.html#Submodel-Options) for the available options for your MCU. 

Under "Build Steps" tap, in "Post-build" area, you need to tell Eclipse to use objcopy to convert the executable file to a binary file. A common usage of "objcopy" is:

```
objcopy -O <output-format> <in-file> <out-file>
```

Refer to this [document](http://manned.org/arm-none-eabi-objcopy) for a complete listing of all options for this command.

---------------

If you can finish all above steps successfully, you should be able to get a binary file that is ready to be burnt to your MCU now.

You might still feel you need more details in the configurations. But I hope you've got the idea how everything works together now. One reason I don't want to include all the details is that I know they will be out-dated soon. And it's almost impossible to list all configuration, which need to be set for successful building, for all types of microcontrollers. Fortunately you can find a lot of articles which include such details. With what you've learned from this article, it's possible for you to understand and adapt the examples you read from these articles to fulfill your own needs.

As mentioned earlier, I will talk about how to get proper startup code and linker script for your Cortex-M microcontroller (if you don't want to write one by yourself) in a separate post.  

