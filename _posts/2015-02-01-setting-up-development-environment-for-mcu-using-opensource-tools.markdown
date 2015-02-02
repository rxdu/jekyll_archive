---
layout: post
title: "Setting Up Development Environment for MCUs with Open-Source Tools (1)"
date: 2015-02-01
comments: true
categories: [Embedded_Development]
---

A lot of articles can be found from the Internet talking about this topic. It looks as if you can easily set up the development environment for MCUs by following these instructions. That can be true if you really understand how everything works inside the process of cross-compiling. If not, you probably will get some problems. The main issue, which makes most of the online articles to be not helpful enough, is that most of the authors just give instructions that are specific to a set of tools with specific versions, not telling you why you need to do each step. Very often you find doing the same thing just doesn't work on your computer, because you're using a different version, or working on a different operating system. You have to Google a lot to find every missing piece to get your tool chain fit and complete.

This situation happened to me when I first tried to set up open-source environment for the development of STM32F4 Discovery board. Before that I had been using IDEs like Codewarrior, AVR-Studio, MDK-ARM and IAR for development of MCUs. These IDEs are convenient and take care of a lot of configuration work for you. But it also means these IDEs hide a lot of details about how tools like compilers and linkers work internally. However, with open-source tools, you have to understand the workflow and figure out how to put all the tools together and get them work properly. If you understand this first, you will find reading the articles I mentioned above becomes more helpful. You will not have to follow them step by step without a clue why you're doing that. Instead you're learning tricks or experience gained for that type of MCU using tool set like GNU toolchain, which are the true values of these articles.

Since I'm talking about this topic myself now, I would like to introduce the workflow of the environment configuration first. I use development of Cortex-M microcontrollers as an example. But you will find the idea is very similiar with the development of other 8-bit, 16-bit microcontrollers.

<center><img src="/img/posts/gnu_toolchain.jpg" width="750" /></center>
<center>Figure 1 Workflow of Cortex-M MCU Development</center>

As shown in Figure 1, you have a few source files and header files(labeled in yellow on the left) in your hand. Usually people start with a blinking LED program, the "Hello World" for the embedded world. To make the code run on the microcontroller, you will also need startup code and a linker script. I will talk about how to get these two files in detail later. Now just assume you've already got these two. Then the four types of files are the input to your toolset. What you want to get is a binary file that can be burnt to and run on your microcontroller, which is labeled in blue in the figure. Getting these files, what your tools will need to do for you:

* C compiler(gcc) compiles source files and header files into assembly files
* Together with the startup file, which is usually written in assembly language, all the assembly files will be passed to the assembler(as) and generated to be object files.
* With the description of linker script, the linker(ld) will link all object files into an executable file. This file can be used for debugging. But it's not ready yet to be burnt into the flash of your MCU.
* Finally a tool(objcopy) will convert the executable file into a binary file which can be understood and executed by the microcontroller.

After finishing the above steps, you've got the file you want for the MCU. Then you will need to use a tool to write it to the flash of the MCU. For the STM32F4 Discovery board, you can use the onboard stlink. For other Cortex-M based MCUs, you can also use tools like Jlink, ARM-USB-OCD to do the same thing. They are all based on JTAG interface. Both hardware(stlink) and software(st-flash) are necessary to do this work. For AVRs, you can use avrdude on the software side and use a USB cable to transfer the file to the MCU, given that you've got a proper bootloader loaded in the MCU already. If you're trying to use a more advanced IDE rather than the Arduino IDE and want to program your Arduino like a normal AVR microcontroller, you will not need to worry about the bootloader because it should have been set up for you when you bought the Arduino board.

So far you should have got an idea what tools you need and what to do with these tools. I will introduce how to make them work in detail in part two of this article.

[Setting Up Development Environment for MCUs with Open-Source Tools (2)]({% post_url /2015-02-01-setting-up-development-environment-for-mcu-using-opensource-tools-2 %})

