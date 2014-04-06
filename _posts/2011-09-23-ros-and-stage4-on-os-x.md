---
layout: post
title: ROS and Stage4 on OS X
comments: true
---
So for my autonomous mobile robotics class I am taking this semester my class project is going to be a new coverage path planner for the Autonomous Lawnmower.  We have decided to develop this planner in simulation and as we surveyed the landscape (MORSE, Gazebo, Stage, and Custom built) we landed on Stage.

Problem though, the stage that comes with ROS didn't work on OS X, but thanks to <a href="https://github.com/rtv">Richard Vaughan</a>'s recent work on <a href="https://github.com/rtv/Stage">Stage4</a>, OS X is back in action as a supported platform.

Another problem, stageros, the wrapper for Stage to interact with ROS, was designed for a pervious Stage API and didn't compile.  So we set out to update rosstage to support <a href="https://github.com/rtv/Stage">Stage4</a>.  We managed to get everything to point where it worked on OS X and Linux.

![Stage4 plus rViz on OS X](/img/ros_and_stage_on_os_x.png "Stage4 plus rViz on OS X")

After spending some time fixing the issues (mostly trivial things) we discovered that Vaughan head already done most of this in the trunk of ROS's stage unary stack, doh.

<a href="https://code.ros.org/gf/project/ros-pkg/scmsvn/?action=browse&amp;path=%2Fstacks%2Fstage%2Ftrunk%2F&amp;pathrev=37480">https://code.ros.org/gf/project/ros-pkg/scmsvn/?action=browse&amp;path=%2Fstacks%2Fstage%2Ftrunk%2F&amp;pathrev=37480</a>

Anyways long story short we managed to get Stage4 and ROS playing nice on OS X and Linux and now our class work can proceed.  The only difference between my changes and Vaughan's was that I decided to resolve the Stage4 dependency with Homebrew rather than in the ROS unary stack.

Here is the brew Formula:

<a href="https://raw.github.com/wjwwood/homebrew/daf127d92166fcd57427e481c7b3c0f746dd3e28/Library/Formula/stage.rb">https://raw.github.com/wjwwood/homebrew/daf127d92166fcd57427e481c7b3c0f746dd3e28/Library/Formula/stage.rb</a>

I recommend using HEAD until a stable tag comes out (`brew install --HEAD &lt;url&gt;`).
