---
layout: post
title: RViz on OS X, Success!
comments: true
---

After working with my friend [John](http://greaterthaninfinity.com/), we have put together a decent one-stop-shop for solving the issues encountered when trying to compile [ROS](http://www.ros.org/wiki/), and specifically [RViz](http://www.ros.org/wiki/rviz) for OS X.  The solution we managed to find is a combination of building all macports as +universal, limiting the system to 1 version of Python (2.6.x for us), and forcing all of ROS to be build as i386 with the `CMAKE_OSX_ARCHITECTURES="i386"` environment variable.  This strategy is based on a comment on a [ticket](https://code.ros.org/trac/ros-pkg/ticket/4788#comment:8) by Dave on the ros-pkg trac.

And here is a snapshot!

![Running RViz on my OS X Macbook Pro](/img/rviz-on-osx.png "Running RViz on my OS X Macbook Pro")

We have our wiki page that details the steps involved on github, here:

[https://github.com/wjwwood/ros-osx/wiki](https://github.com/wjwwood/ros-osx/wiki)

Most of the things on the wiki are solved problems that are either tickets that have been solved up stream but haven't been backported to diamondback yet, or are simple tricks to getting ROS, and macports to play nice.  Hopefully the guide won't even be necessary once [Electric Turtle](http://www.ros.org/wiki/electric) is released.

I am very pleased with the performance(~20% cpu use on data in screenshot below), but there are still some usability issues, some of which I have noticed on my VM's too, I have been keeping track of them and I hope to make tickets for them soon and maybe even try patches for them.
