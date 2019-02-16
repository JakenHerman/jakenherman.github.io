---
layout: post
title:  "Implementing Apache Cordova Push Notifications in Android using Firebase"
excerpt: "Firebase Cloud Messaging (or FCM) is a great cross platform messaging solution that is completely 100% free. Today, I’ll walk you through the process of creating push notifications in your Android Apache Cordova application using Firebase."
comments : true
date:   2019-02-11 18:39:39 -0600
categories: [JavaScript, Mobile Development, Firebase]
---

Firebase Cloud Messaging (or FCM) is a great cross platform messaging solution that is completely 100% free. Today, I’ll walk you through the process of creating push notifications in your Android Apache Cordova application using Firebase.

> Prerequisites :
>
 > * Have a Firebase account (it’s free, just go sign up!)
 > * Have npm/cordova installed on your machine.

The first thing we’re going to do is set up a cordova project. If you already have your project set up, skip this step. I’m including it for completeness. We’re going to create this project in our desktop directory, so first you should open up your terminal or command line and type “cd desktop”. Next, type `cordova create notificationtest com.notificationtest.app`. Be sure you get the `com.notificationtest.app` part as that is our package name that Firebase will use. Type `cd notificationtest` to change to your new project directory.

The next thing we’ll do is add the Android platform to our newly created Cordova project. Type `cordova platform add android`, and this will set your project up to be able to run on the Android platform. The next thing we’ll need to do is install a plugin for Firebase to interface with our project. GitHub user arnesson has created a great plugin for this, and we can install it by running the command `cordova plugin add cordova-plugin-firebase --save`.

Now we can go into Firebase and select “Add project”. Type “Notification Test” (or your project’s name) into the Project Name area, and select Create Project. Now that your project has been created, go to the Project Overview page for your Firebase project and select Add app, and select the Android logo.

Now you’ll be able to register your app. In the Android package name section, type com.notificationtest.app, and press Register app. This will generate a JSON file called `google-services.json`. Download this file, and continue through the App registration page, just selecting the things that are selected by default.

Navigate to the directory where the `google-services.json` file was downloaded, and move the file into your `desktop/notificationtest` directory.

Open your terminal back up and type `cd desktop/notificaitontest`. Then type `cordova run android`. This will start up the Android emulator running your application. The next thing we need to do is set up a cloud message in Firebase. On your Firebase project page, scroll down to the “Grow” section, and select “Cloud Messaging”. If you’ve never created a notification before, the button text will be Create your first message, and if you have created a notification before, the button text will be New notification. Press the button, and under Notification text, type “Hello World!”, and press “Next”. In the Target section, select NotificationTest for your app, and press Review. A modal will appear of the notification you’re preparing to send. Select the blue Publish button to fire your notification away!

And that’s it. You’ve just sent your first push notification. Congratulations. If any of this was difficult to follow, feel free to watch the YouTube video I made of it below. Thanks for reading.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tx09AElYnzE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>