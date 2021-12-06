Coursera-Introduction to Embedded Systems -Assignment2-GNU-Make-and-GCC-

Exploring Make GCC tools Author: Mustafa Tayyip BAYRAM Date: 28/09/2020

> The make file is in src directory. #USE $make build PLATFORM=MSP432 or $make build PLATFORM=HOST to build  

> This Assignment is my solution to Coursera's Embedded Software Essentials course specialization, module 2.  
  Familiarizes with GNU's gcc, Make, size, objcpy and objdump utilities.

> In this programming assignment you will create a build system using the GNU tools, GCC and GNU Make. This assignment will require you to >

#### After completing this assignment, you will be able to:
Use GCC and GNU Make to create a command line build system 2) Write a makefile that can natively and cross compile an application 


In this programming assignment you will create a build system using the GNU tools, GCC and GNU Make. This assignment will require you to compile multiple files, link them together and create a final output executable. Some files will be provided for you, but you will need to support two platforms; the host environment and the target embedded system MSP432. The host system will allow you to simulate software on a host platform. The target system will be used in upcoming assignments as we begin to create our microcontroller applications.

