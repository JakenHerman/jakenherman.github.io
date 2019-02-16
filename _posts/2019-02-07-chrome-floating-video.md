---
layout: post
title:  "Enable Floating Video in Google Chrome"
excerpt: "This one line of JavaScript allows you to have a floating Google Chrome window to watch YouTube, Twtich, and other media sources while you're working."
comments : true
date:   2019-02-07 18:39:39 -0600
categories: [Chrome, Tips and Tricks, JavaScript]
---

If there is one thing the Opera browser has done correctly, it is that it made creating a floating video pop-out very easy and accessible to it’s users. If there is anything else it has done correctly — I don’t know about it. I’d just much rather use Chrome.

If you’re like me, when you’re doing simple work or playing a casual video game, you like to watch YouTube or Twitch while you’re at it. The problem? Having a window with YouTube or Twitch gets put in the background the minute you re-enter your work pane or game window. The old solution was to just have your work be snapped to one side of your screen and your video on the other side. That’s not good enough for me.

The correct solution? A bookmark with one line of JavaScript in it.

To get started, right-click your bookmarks bar and select “Add page…”. For the Name type “Float Video”, and for the URL, paste the JavaScript line below:

`javascript:document.getElementsByTagName('video')[0].requestPictureInPicture();`

Once you’ve got your bookmark created, you can navigate to a YouTube video or Twitch stream, maybe even Netflix (haven’t tested this), and press your new “Float Video” bookmark.

Your video will pop out in a floating video Picture-in-Picture style and when you return to your work or video game, you will have your re-sizable, movable video hovering over your main window.