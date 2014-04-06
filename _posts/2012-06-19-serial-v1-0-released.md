---
layout: post
title: Serial v1.0 Released
---
After several months of work, Serial v1.0 is out!  Serial is Cross-platform serial (rs-232) library written in C++.  You can grab it at my github page:

[http://wjwwood.github.com/serial/](http://wjwwood.github.com/serial/)

Or you can browse the documentation:

[http://wjwwood.github.com/serial/docs/v1.0/index.html](http://wjwwood.github.com/serial/docs/v1.0/index.html)

A short list of the features:

- Windows, Linux, and OS X support
- Permissive license ([The New BSD License](http://www.opensource.org/licenses/BSD-3-Clause))
- Support for custom baudrates (where supported)
- Flush the I/O separately, and block until writing is complete
- Control handshaking lines
- Block for changes in handshaking lines (Linux and Windows)
- Complete timeout control (interbyte, per call, and per byte timeout components)
- Minimal dependencies (cmake)
- Support for ROS (ros.org) as a unary stack

For many months now, my friend John ([http://greaterthaninfinity.com/](http://greaterthaninfinity.com/)) and I have been working on a cross platform serial library written in C++.  We surveyed the web and found that there really wasn't a well designed and easy to use serial library that made any effort at being portable (Windows, Linux, OS X).  We really like PySerial and we wanted something as simple and straight forward as that for C++.  Initially we found that Boost had good portability in its serial library, part of boost.asio, but it was verbose and over complicated, and still didn't provide portability for actions like, flushing the serial port, setting the hand shaking lines, etc...  So we set out to write one from scratch with a custom built unix and windows implementation, and an ABI compatible single interface modeled after PySerial, but with a few changes.  Most notably is that the timeout system mimics the Windows serial timeout struct, and therefore has five parameters for controlling read/write timeouts.  This behavior is achieved in Unix systems by using select to figure out when to read, rather than relying on Unix's read command for timeout behavior, which exactly how PySerial does it.

I am really excited to see it finally out, and there are several people outside of our lab here at Auburn already using it, and finding bugs =p (v1.0.1 is due out soon).  If you decide to give it a whirl and find problems please open an issue on github: [https://github.com/wjwwood/serial/issues/new](https://github.com/wjwwood/serial/issues/new)
