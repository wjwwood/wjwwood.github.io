---
layout: post
title: Received Structure.io Device
comments: true
---

On Friday I finally received my [Structure.io](http://structure.io/) device from my backing them on Kickstarter!

Obviously I wanted to see if it worked with the openni2 ROS drivers, so plugged it into my MacBook and ran the `openni2.launch` launch file in the `openni2_launch` package. I was easily then able to then subscribe to the depth image using `rqt`'s `Image View` plugin:

![Structure.io device]({{ site.url }}/img/structure-io-device.png)

I ran into some trouble getting the point clouds to publish, but I think that has to do with some assumption about the device that the ROS driver is making. I think it may be assuming that it has a color camera and so it will try to output colored point clouds. I am not 100% certain about that, but I will probably try to dig into the issue at some point now that I have the device in hand.

I guess I shouldn't be surprised that it mostly worked out-of-the box, but it is exciting to me because I think this device could make an excellent alternative as a robot sensor because it is smaller than even the ASUS Xtion's, it doesn't have a color camera (which in many cases is not needed for a small robot), and it is designed to be mounted to things. In fact the Structure.io guys have CAD files for the device so you can 3D print your own mounts for it.

I have been slowly accumulating pieces for a robot and I think this might be the obstacle avoidance sensor for that project when ever I really get it going.
