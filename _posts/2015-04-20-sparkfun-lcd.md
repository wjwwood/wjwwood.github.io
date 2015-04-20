---
layout: post
title: SparkFun LCD
comments: true
---

I've had this SparkFun LCD break lying around for a long time.
I think I ordered it back in 2010 along with my mbed and never took the time to get it working.
I was doing some electronics stuff today and I noticed it in my electronics tackle box and I thought I'd give it another go.

First off, this is the board I'm talking about:

[https://www.sparkfun.com/products/retired/8600](https://www.sparkfun.com/products/retired/8600)

I was able to pretty quickly find a library called `gLCD` which let me get it going pretty easily.
I did run into trouble compiling it, but it was easy enough to fix up.
However, the source was not in any VCS I could find (I downloaded it from [http://www.railways-in-miniature.co.uk/gLCD.zip](http://www.railways-in-miniature.co.uk/gLCD.zip)).
So I "forked" it into a repository on my GitHub account and pushed the origin code and afterwards my patch which gets it working on Arduino versions >= 1.0:

[https://github.com/wjwwood/arduino-glcd](https://github.com/wjwwood/arduino-glcd)

After getting it to compile, I should mention I was compiling the `TestPattern` example which comes with the library, I reasoned out how to wire it up to my Arduino Mega that I was using.
I connected things according to this:

```c++
//You can use these variables to set the pin numbers
const char RST = 8;
const char CS = 9;
const char Clk = 13;
const char Dat = 11;
```

And additionally I connected `vin` to my 3.3v pin on the arduino and the `vbatt` to the 5v pin.
Then it just worked:

![gLCD driving a Test Pattern]({{ site.baseurl }}/img/sparkfun_lcd/test_pattern.jpg)

So that's neat, but I was doing some more digging around and noticed this thread:

[https://forum.sparkfun.com/viewtopic.php?f=15&t=15448](https://forum.sparkfun.com/viewtopic.php?f=15&t=15448)

In summary, there is an inductor on the board (it's blue with `221` written on it) which gets really hot:

![Small blue inductor]({{ site.baseurl }}/img/sparkfun_lcd/inductor.jpg)

And sure enough I touched my finger to it and it was hot!
The conclusion on the forum was that it should be replaced with an inductor which can handle more current (around ~500ma).
But another suggestion was to replace one of the resistors with a different value, which some reported helped.

I ran out of time to actually try that, but maybe I'll give it a go next time I pull it out of the box.
