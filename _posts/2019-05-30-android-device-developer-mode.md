---
layout: post
title:  "How to put your Android device in Developer Mode"
excerpt: "Developer mode unlocks options for USB debugging"
comments : true
date:   2019-05-30 08:00:00 -0600
categories: [Android, Learning, Tips and Tricks]
---
If you are a mobile developer like me, you need to have your device in developer mode in order to run your builds on something other than the extremely slow Android emulators provided by Android Studio. The problem is, the way to enable developer mode on your Android device is a bit cryptic.

First, open your device's settings app. Before developer options becomes an available setting, we first must find the phone's build number, and this is typically in a group called something like **Software Info** or **About Phone**. On most Android devices, you will be able to search for "Build Number", and you will get exactly what you are looking for. 

Now that you have found the build number screen, you will need to tap on the *Build Number* field **seven** times. Once you start tapping the build number, a small alert will prompt you saying *You are now # steps away from being a developer*. The number will count down every time you tap the field, until you have reached **seven** taps, at which point the prompt will display *You are now a developer!*

Now that you are a developer, the "Developer options" will be available to you as an option in Settings. Now you'll be able to enable things like USB debugging, WebView implementation, Bluetooth HCI snoop logging, and more. To get to developer options, search in your settings for "Developer options".

To turn developer options back off, just flip the switch at the top of the developer options screen to "off". Once you navigate away from this screen, it will be gone from your phone until you repeat the above steps to enable developer mode.
