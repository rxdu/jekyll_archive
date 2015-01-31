---
layout: post
title: "Use STM32 Peripheral Library with emIDE"
date: 2014-01-21 22:22:27 -0500
comments: true
categories: [STM32, Embedded]
---

emIDE is a open source IDE for embedded development. It integrates GCC toolchain and provides JLink support for debugging. Compared with other free, open source alternatives, it's much easier to start with. This blog introduces how to configure emIDE to write programs for STM32 MCU with standard peripheral library. The MCU used in this example is *STM32F103T8*. The library used is *STM32F10x\_StdPeriph\_Lib\_V3.5.0* from ST. And the debugger probe is JLink EDU.

<!-- more -->

* First download STM32F10x\_StdPeriph\_Lib\_V3.5.0 from the website of ST. Extract the archive file and you will get a folder which includes: *\_htmresc*, *Libraries*, *Project* and *Utilities* folders. 
* Start emIDE and create a new project. Choose a directory to save the project and select the device you are using during the creating process. By default, you will get 3 folders in the project: *Doc*, *Setup* and *Src*. Setup folder includes a linker script and a startup code for the MCU. You can add your own code into Src folder.
* Copy *Libraries* folder (from step 1) into the project directory. Copy *main.c*, *stm32fx\_conf.h*, *stm32f10x\_it.c*, *stm32f10x\_it.h* from *Project\STM32F10x\_StdPeriph\_Template* (from step 1) to *Src* folder. Do not copy system\_stm32f10x.c to Src, otherwise you will get multiple definition error during compilation. Add all files mentioned above including files in *Libraries* folder into your project in emIDE. Then remove *startup* folder (Libraries\CMSIS\CM3\DeviceSupport\ST\STM32F10x\startup)  from the project since emIDE has already provided a linker script and startup code in *Setup* folder. The structure of the project will look like the following screenshot.

<img src="/img/posts/emide_1.png" width="400" />

* In "Build Options" of the project, under Compiler *settings/#defines tab*, add two macros: STM32F10X\_MD, USE\_STDPERIPH\_DRIVER. The first one specifies the MCU family you are using and the second one tells the compiler you will use standard library in the project.

<img src="/img/posts/emide_2.png" width="600" />

* Add Search directories so that the compiler can find all header files of the library.

<img src="/img/posts/emide_3.png" width="600" />

* In Properties of the project, make sure your JLink works under the right mode.

<img src="/img/posts/emide_4.png" width="600" />


Now you should be able to build the project and download the code into your target board.


