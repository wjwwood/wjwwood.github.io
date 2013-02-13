---
layout: page
title: Hello There!
tagline: Welcome to my website!
---

{% include JB/setup %}

My name is William and I am a software engineer with a passion for open source robotics.  I have worked on robotics projects through out college and at robotics companies like [Willow Garage](http://www.willowgarage.com/).  I am an active member of the [ROS community](http://ros.org/wiki/) and a core developer for the core [ROS stacks](https://github.com/ros/).  I have been helping design and build the [development tools](https://github.com/ros/catkin/) and [infrastructure tools](https://github.com/ros-infrastrucutre/) used by the ROS community.

Please checkout my [projects](projects.html) or enjoy my ramblings:

<span>
{% assign posts_collate = site.posts %}
{% include JB/posts_collate %}
</span>
