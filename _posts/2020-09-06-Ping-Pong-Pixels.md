---
layout: post
title: "Ping Pong Pixels - Modular RGB LED Lighting"
summary: Ping Pong Pixels were an idea I had a long time ago but took forever to get around to actually designing and building. The idea is super simple... create a modular 3D printable "chassis" for housing RGB LEDs, along with a diffuser (in this case a ping pong ball), and make them able to connect in various ways so you can create all different shaped lighty-uppy-stuff. The initial version just lets you create different size/ratio matrix grids, but I've also got an iteration in the works that lets you do cylindrical lamps, spherical lamps, and more.
tags: [Hardware]
twitter: 
github: 
cover: /images/2020-09-06-Ping-Pong-Pixels-Cover.png
---

Ping Pong Pixels were an idea I had a long time ago but took forever to get around to actually designing and building. The idea is super simple... create a modular 3D printable "chassis" for housing RGB LEDs, along with a diffuser (in this case a ping pong ball), and make them able to connect in various ways so you can create all different shaped lighty-uppy-stuff. The initial version just lets you create different size/ratio matrix grids, but I've also got an iteration in the works that lets you do cylindrical lamps, spherical lamps, and more.

![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-10.jpg)

I initially played around in Fusion 360 trying to come up with a way that would let you connect multiple modules together on any edge, without having to use hardware/bolts or anything else. The idea is you should be able to just print everything and keep it as minimal as possible while still being strong enough to stay together and be moved around without all falling apart. It took a fair few iterations to nail it, but the final result is actually quite impressive and I've got lamps around the house now that have held together for over a year, even with kids playing with them and moving them.

![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-1.png)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-2.jpg)

Using ping pong balls as diffusers wasn't my idea (credit goes to [Bitluni](https://www.youtube.com/watch?v=fz2QAV9z_o8&t=1s) for that one) but from my searching around at the time I seem to have been the first to come up with the idea of making it modular, rather than huge sheets of wood drilled out as a single large matrix. I'm really into having lots of little RGB decorative lamps around the house as mood lighting, so I just wanted an easier way to do this for myself.

The ping pong balls are cut out by placing them on one of the chassis pieces and tracing a circle with a marker, and then using a scalpel to cut around your line. I played with 3D printing jigs for drillpresses, making adapters for soldering irons to try burn the holes, and lots of other methods... but at the end of the day it was actually fastest just to practice and get good at cutting the little circles out by hand. They generally only take a few seconds each now.

![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-3.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-4.jpg)

Next, you feed in your strings of WS2811s (or any similar LEDs) and they "click" into the holes perfectly, to the point where I ended up not even using hot glue or anything to hold them, although it doesn't hurt to glue them if you want extra strength.

![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-5.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-6.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-7.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-8.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-9.jpg)

Software-wise I run them all on [WLED](https://github.com/Aircoookie/WLED) which is an incredible piece of open-source firmware for ESP8266 and ESP32 microcontrollers that lets you control WS2811/WS2812/etc RGB LEDs. It comes with dozens/hundreds of different pre-build animations, each infinitely adjustable with colour presets, timing/intensity presets, and a full API along with all sorts of integrations such as Home Assistant and lots more. It even has a [browser-based installer](https://install.wled.me/) that lets you flash your ESPs directly, thanks to Web Serial.

I've since made about half a dozen of these lamps in various sizes/shapes over the last year or 2, and have a lot more in the works for this project so I'll update it (Soon™) when I have more to show.

![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-11.jpg)
![Ping Pong Pixels](/images/2020-09-06-Ping-Pong-Pixels-12.jpg)

