---
layout: post
author: Sen
title: "Arcade Macro Board for OBS"
tags: [diy, hardware, software]
categories: hardware
twitter: https://twitter.com/senwerks/status/1260202069325049859
github: https://github.com/senwerks/arcade-macro-keyboard
image: 2020-05-15-Arcade-Macro-Board-ArcadeMacroKeyboard1.jpg
---

Since the coronapocalypse kicked in and we've all been isolated, I've been doing a lot of Jitsi meets with various groups of friends. We'll get togther for a video chat, and thanks to [OBS (open source broadcasting software)](https://obsproject.com/) we can do things like sharing our screens to each other with our webcam overlayed, or play a game and share that with each other, and lots more. In OBS you set up "Scenes", which are basically layouts of what you want to show each other. One might be your webcam view of yourself placed in the corner of a screen showing your coding IDE, so you can show code you've been working on. Another might be the screen showing a game you're playing. It's the software used by almost every single Twitch/YouTube streamer and live online show, and it's extremely powerful software considering it's completely free.

One thing streamers do which I thought would also be useful for our private video chats is to buy a [Stream Deck](https://www.elgato.com/en/gaming/stream-deck), which is a physical panel of buttons that let you quickly change Scenes in OBS without having to change back to your OBS window or fiddle with your mouse. It's a very handy piece of equipment, but considering i'm not a streamer and have no real intent to ever be one (I don't even like mirrors), I can't really justify forking out the cash for a product like that. So... we make one (the below is a copy/paste from the Github):

# Arcade Macro Keyboard

Github: [https://github.com/senwerks/arcade-macro-keyboard/](https://github.com/senwerks/arcade-macro-keyboard/)

A macro keyboard made of arcade buttons. Acts like a normal USB keyboard, but each arcade button runs multi-key macros/shortcuts.

## Example Use

I use it as a Stream Deck using OBS for Twitch/YouTube streaming and Jitsi video calls. I set the "keyCodes" in the code to numbers 1-7 (ASCII 49-55), and the modifiers to CTRL, ALT, and SHIFT. Pressing arcade button 1 then sends the macro CTRL+ALT+SHIFT+1 to Windows, which I have mapped in OBS to switch to Scene 1. Etc etc.

It will work everywhere in Windows, not just OBS/Jitsi/etc, and just acts like a standard USB keyboard inserting the shortcuts as though you yourself pressed it on your primary keyboard. You could use it to run macros/combos for your games, or for photo/video editing, or whatever you want.

Number of buttons doesn't matter, you can do more or less, as long as you have enough inputs and modify the code appropriately to add/remove them. Diagram below shows 8, but the code here is currently set up for 7 as that's all I ended up using.

## Wiring Diagram

![Arcade Macro Keyboard Diagram](/images/2020-05-15-Arcade-Macro-Board-WiringDiagram.png)

## Installation

- Load the code onto your Arduino Nano
- Plug the USB cable into your PC
- Open up your OBS Settings and go to Hotkeys (this assumes you already have scenes set up)
- Click on each of your scene's "Switch to Scene" entry, and press one of the buttons on the macro board to insert that button's shortcut combo

![OBS Hotkeys](/images/2020-05-15-Arcade-Macro-Board-MappingButtonsInOBS.png)

- Click OK

## Arduino

Want to use the Arduino IDE instead of VS Code? The .cpp file in /src should work fine as-is (embedded below), or you can visit the [Arcade Macro Keyboard Sketchbook](https://create.arduino.cc/editor/obsoletenerd/15b42f98-5e19-4aff-b1d9-8078c02f6f8f/preview) on Arduino.cc to install the code directly from the browser to your Arduino Nano. 

<script src="https://gist.github.com/senwerks/c0ca22b73e6c3040dd16fd8d8b610856.js"></script>

## Photos

3D printed case STL is [included here](https://github.com/senwerks/arcade-macro-keyboard/blob/master/ArcadeMacroKeyboardCase.stl), but it's very basic. Print it top down, no supports or anything needed. I'll probably design a nicer one at some point.

![OBS Hotkeys](/images/2020-05-15-Arcade-Macro-Board-ArcadeMacroKeyboard1.jpg)

![OBS Hotkeys](/images/2020-05-15-Arcade-Macro-Board-ArcadeMacroKeyboard2.jpg)

![OBS Hotkeys](/images/2020-05-15-Arcade-Macro-Board-ArcadeMacroKeyboard3.jpg)
