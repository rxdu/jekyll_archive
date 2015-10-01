---
layout: post
title: "MCU Programming Tips"
date: 2015-05-26
comments: true
categories: [[C/C++,Programming]]
---

Here are some tips that might be helpful to improve your code for microcontrollers. It's not a complete list but most of the issues mentioned here are commonly seen during the lab sessions of ECE2049 at WPI and probably from any code by new embedded programmers.

**Program Structure**

* Always think first before writing code

Some students may feel so excited that they want to try something out even before they finish reading the lab instructions. It may seem to be a waste of time to do some careful thinking, draw flow charts before starting working on the project. Unfortunately it's not true unless you're just writing "really really simple" programs. Even for projects like the simplified "space invader", it's worthy of spending some time to get a blue print in your mind first.

* Modular design

First get a big picture of the whole program. Think what kind of data structures you need to use and approximately how many modules you need to divide your program into. The design phase of a real-world project can take days, weeks or even months. Probably you don't need that much time for your lab projects, but definitely you need to do it. Another benefit of modular design is that it can be easier for you to reuse your code in the future. You spend time implementing a function and why just throw it away after one-time use?

* Learn how to separate declaration and definition by using header files

It's common that you need to collaborate with others on a project. For big projects, it's unnecessary for everyone to know each other's implementations. But you need a way to expose your functions to others so that they can call a function you write to do some calculations. Moreover, a single file project is difficult to maintain and the readability is terrible. You can find a good guide [here](http://www.umich.edu/~eecs381/handouts/CHeaderFileGuidelines.pdf).

* Use state machines to control a complicated process

Using a state machines can help you to avoid deep if()/else() statements. Remember that you can use multiple level state machines if a state of your state machine is very complicated.


**Variables**

* Only ask for what you need, no more no less

A microcontroller has very limited hardware resource and as a embedded programmer you should always keep this in mind. If you have experience using a low-end Arduino before, you may have seen such problems that your code suddenly behaves in a weired way after you import some libraries, to drive a wireless adapter for example. It's very likely to be a memory issue. So keep good habits and avoid asking for more than what you need from the system, even if the hardware still can provide more.

* Be familiar with the range of each data type

Make sure you don't assign a value that is bigger than a type of variable can accept. Also don't waste the memory space. For example, in most cases the indexer for a "for loop" will not be a very large number, so a 8-bit unsigned char type should be enough, then don't use an unsigned int, which is 16-bit long (for MSP430 in CCS). Read this interesting [article](http://betterembsw.blogspot.com/2015/05/counter-rollover-bites-boeing-787.html) about counter rollover issue on Boeing 787.

* Be aware of the signedness of the variables

if(x - 20 < 0) can behave differently with if(x < 20). Why? If x is of an unsigned type, then even if x is smaller than 20, you will not get a true condition from the first if statement.

* Get used to bit manipulations

If you want to store the state of 8 LEDS, it's a better option to just use a single 8-bit unsigned char variable, of which each bit represents the state of one LED, instead of 8 variables or an array.

* Follow naming conventions

It cannot only make your code look more professional but also prevents you from making mistakes. For example, with proper naming you can easily tell if a variable is constant or not and avoid assigning a new value to a constant after declaration. You can refer to the [Google coding style guide](https://google-styleguide.googlecode.com/svn/trunk/cppguide.html).

* Limit the use of global variables

A lot of global variables usually mean your functions/modules have very tight couplings, which can make the maintenance very difficult at a later phase. You also need to consider the synchronization if your program runs with interrupt routines. When you use RTOS, usage of global variables can make a function non-reentrant. Think it this way: you are manipulating a global variable a in your function and at that specific time the value of a is A1; before you can finish the calculation an ISR jumps out and changes the value to be A2; now your functions returns but continues the calculation with a different a variable. What can you expect to get from that function?

* Control the scope of your variables

If a global variable is only used within a single module, then don't expose it in the header file. Declare it in the source file and you can also use the "static" key word to make sure it cannot be used anywhere other than this .c file.

**Functions**

* Don't make your functions too long

If a function starts growing big, think about how you can make part of if to be another function. Do unit test of a smaller function and then combine them together to finish something more complicated.

* "Again" modularity design

Group your functions into separate modules and only expose necessary information from header files. For example, you can have a module that does hardware initialization: msp430_init.c and msp430_init.h. You can implement functions like TouchPadInit(), LEDInit(), ButtonInit(), TimerA2Init() in the source file and expose them in the header file. Then for any subsequent labs, you can just copy this module, modify the initialization slightly according to changed requirements and you're reusing your code! For functions of operating LEDs, you don't need to change anything.
