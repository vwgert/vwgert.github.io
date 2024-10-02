# Preface
Linux plays a crucial role in diverse applications, from smartphones and web servers to tablets, IoT devices, smart washing machines, self-driving cars, modems, routers, and even gaming consoles like PlayStations. In essence, Linux is far more pervasive than one might initially imagine. This book comprehensively explores essential topics for initiating your journey with Linux as an operating system, providing insights into navigating through a command-line interface (CLI). Notably, this book serves as the curriculum at PXL University College in Hasselt, Belgium, where it is employed to instruct first-year computer science students on Linux fundamentals.

For a digital version of this book, visit [https://d-ries.github.io/linux-essentials/](https://d-ries.github.io/linux-essentials/). This platform also offers hands-on labs and exercises, providing practical opportunities to reinforce your understanding of the concepts discussed in this book

# Introduction

## Linux
Windows, made by Microsoft, is a well-known Operating System mostly used on Desktop computers, but there are other alternatives as well. One of the more popular ones are MacOSX, ChromeOS and, of course, Linux. Linux, using a desktop environment, is less prominent than the others.

In Server / IOT / mobile environments, a certain shift in used Operating Systems occurred. Linux is one of the most popular operating systems in these markets. Some interesting statements:

* Most supercomputers run on Linux

* The most popular cloud infrastructure providers use Linux
![tux, the Linux mascotte](../images/tux.png)


Linux is used in smartphones, (web) servers, tablets, IoT devices, Smart washing machines, self driving cars, modems, routers, PlayStations, ... In brief: Linux is used way more than you would initially think. Linux even has its own mascotte, the penguin named Tux!

## Unix
Dennis Ritchie and Ken Thompson created the Unix operating system in 1969. The source code from this OS was shared at that time. After a while the company AT&T Bell Labs decided they wanted to sell Unix commercially. BSD further developed the Operating System independently from Unix. This led to subsequent versions:

* Unix: The commercial version

* BSD Unix: The open source version


In the '80 there were different versions of Unix. Because Unix was commercialized (AT&T), the source code of Unix was rewritten: GNU project ("GNU is not unix"). The goal of GNU was the development of an open source Operating System where everyone could work on together as a community. The GNU project was missing a kernel.

## Linux
A student, named Linus Torvalds, created a post in a newsgroup about his own Operating System in the '90:

![a post by Linux Torvalts](../images/01/linus.png)

We are still using the Linux kernel today. The kernel is being further developed every day.  

* The history of Linux - Timeline 1([https://en.wikipedia.org/wiki/Linux#/media/File:Unix_timeline.en.svg](https://en.wikipedia.org/wiki/Linux#/media/File:Unix_timeline.en.svg))

### Linux distributions
Linux distributions (distros in short) simplify the process of installing gnu/linux and other apps on your computer. Well-known distros are Ubuntu, RedHat, Fedora, CentOS, Debian, Archlinux and Oracle Linux. Because linux is very scalable, there are also special distros for a certain purpose, for example clonezilla.

For this book we will focus on Ubuntu ([https://ubuntu.com](https://ubuntu.com)), a very popular debian based distribution made by Canonical.

## Installing Ubuntu
While it is possible to install Ubuntu Server/Desktop directly as the main operating system on your laptop/desktop, for learning purposes, we recommend running the operating system in a virtual environment such as VirtualBox. To get started with Ubuntu in a virtual environment, you will need to:

* Download the Ubuntu Server ISO image from the official Ubuntu website ([https://ubuntu.com/download/server](https://ubuntu.com/download/server)).

* Install virtualization software, such as VirtualBox, on your host machine.

This book does not cover the installation of Ubuntu Desktop. Numerous online guides comprehensively address this topic. However, the digital version of our book does include a section on installing Ubuntu Server in VMWare ([https://d-ries.github.io/linux-essentials/#/./02_installation/01_course](https://d-ries.github.io/linux-essentials/#/./02_installation/01_course)). Please note that the steps may vary slightly for VirtualBox or any other virtualization platform. Alternatively, you can explore installing Ubuntu on the Windows Subsystem for Linux, abbreviated as WSL2 ([https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview](https://ubuntu.com/tutorials/install-ubuntu-on-wsl2-on-windows-10#1-overview)).

