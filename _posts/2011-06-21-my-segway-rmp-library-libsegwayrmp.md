---
layout: post
title: "My Segway RMP Library: libsegwayrmp"
---

I have been working a library for interfacing with the Segway RMP series of mobile robots.  You can find the source online at <a href="https://github.com/segwayrmp/libsegwayrmp">https://github.com/segwayrmp/libsegwayrmp</a>, and the documentation at <a href="http://segwayrmp.github.com/libsegwayrmp/">http://segwayrmp.github.com/libsegwayrmp/</a>.  I decided to take this step because I needed several things in a rmp library that I couldn't find all in one place.  Those things included:

# Cross Platform

I do all my work on Linux computer, but I like to use my Mac when ever possible as well, but also we have some projects here that run on Windows still and I need to be able to support that too.  Most of the libraries I looked at had a pretty one-off feel to them and therefore only worked on one OS.  A few libraries had some polish but still lacked support for Windows and Linux in the same library.  Sadly, I cannot say for certain that my new library works on Windows yet, but there is absolutely no reason it shouldn't and I just need to test it out and fix any small problems I run into.  The big difference is that my library considered cross platform portability from the beginning, so even if I don't use it on Windows for some time, there is no glaring incompatibility that will keep it from running on Windows when the time comes.

# Open Source

For most of the libraries I looked at this isn't a problem as they are generally GPL or BSD, but I like to stay away from GPL when possible.  To that end my library is permissively licensed under the BSD license.  For those who don't know that means copy it, use it, sell it, integrate it, just mention you got it from my library.

# Support both Serial and USB

This is the big one, there are basically three ways to interface with the Segway RMP: CAN, USB via FTDI's D2XX Library, and Serial.

## Interfacing with CAN

In order to interface with the RMP via CAN you needed to have an older model that came with a third party CAN2XXX device for linking it to your computer.  I have seen systems that use the kvaser CAN interfaces and others that used the popular PCAN  interfaces.  Either way, this is an old and outdated method for interfacing with the RMP's and now they all have USB connections that provide access to the CAN bus through a USB packet interface using an FTDI FTD245BM Chip.  Since this is an out of date method and there many different interface specific concerns, my library doesn't support CAN directly, though my generic RMPIO class allows for easily making a CAN interface work.

## Interfacing with USB

The USB interface that now comes on all Segway RMP's is made possible by the FTDI FTD245BM Chip used in the "UI" component of the RMP these days.  If you aren't familiar with the way that the FTDI driver system works there are basically three different ones for most of their devices.  First there is the D2XX driver.  This driver provides only a USB (now libusb based) interface to the chips, which gives the programmer much more in depth control and access to FTDI chip specific commands and provides a, presumably, more efficient interface for reading and writing to the serial like devices.  This is in contrast to the VCP driver from FTDI, which allows the Operating System to use the FTDI device like a legacy com port, showing up in Windows like 'COM1' and in POSIX like '/dev/ttyUSB0' or similar.  This is now the default type of interface in Linux and in fact you have to forcefully remove and blacklist the ftdi_sio and usbserial drivers in the kernel to prevent the VCP style representation of the device.  This was problematic for me because I use Linux for everything and most all of the libraries only supported the D2XX style interfacing for the RMP.  Therefore I had blacklist the ftdi_sio driver from capturing the device, but this is a blanket operation, meaning that any other FTDI devices would also not show up as serial ports.  I didn't like this.  The last type of driver is Windows only and is called the CDM (Combined Driver Model) which allows for dynamic switching from VCP to D2XX.

## Interfacing with Serial

Like I said, the fact that using the RMP as a USB device on Linux meant that I couldn't use other FTDI devices like serial ports was a potential deal breaker for me.  There for I set out to write a driver for the RMP that would use the VCP style interface for communication.  I did this, using my <a href="https://github.com/wjwwood/serial">serial library</a>, and I was successful after only a week or so.  But, I realized that I couldn't use the VCP driver on Mac... So I decided to add the ability for my driver to optionally use either USB or Serial to interface with the RMP.  This took more time, but finally I have a solution for right now and I plan to add more of the features I wanted later.

# Other Design Considerations

In addition to the things I was looking for in a library, capability wise, I needed to consider something else.  I originally wanted to just extend someone else's library, but I considered the fact that it wasn't exactly without baggage.  To be fair my library has a dependency on my homebrew serial library, but it is optional and easy to install.  I needed my library to work in a monolithic stand-alone application, in a <a href="http://www.ros.org/wiki/">ROS</a> package (for my work), and a <a href="http://www.robots.ox.ac.uk/~mobile/MOOS/wiki/pmwiki.php">MOOS</a> Application in another svn repository (for my co-workers).  Therefore I took great care in designing the build system in particular to be flexible, portable, and gracefully degrading.

Watch here for a <a href="http://www.ros.org/wiki/">ROS</a> package: <a href="https://github.com/segwayrmp/segway-rmp-ros-pkg">https://github.com/segwayrmp/segway-rmp-ros-pkg</a>

For the <a href="http://www.robots.ox.ac.uk/~mobile/MOOS/wiki/pmwiki.php">MOOS</a> Application, email me.

For the monolithic-application, email me.

# Results

To recap I wanted several things for my new Segway RMP library and here is where it stands:

- Open Source:
    - BSD Licensed
- Cross-Platform Support:
	- Linux
	- Mac OS X
	- Windows (Needs testing)
- Multiple Interface Types:
	- CAN (Will not support, unless someone asks and has hardware to test it with)
	- USB (Supported on Linux, Mac, and Windows (needs testing))
	- Serial (Supported on Linux, Mac, and Windows (needs testing))

I hope that this library will help others at some point and don't be afraid to ask questions or post bugs on the tracker: <a href="https://github.com/segwayrmp/libsegwayrmp/issues">https://github.com/segwayrmp/libsegwayrmp/issues</a>.
