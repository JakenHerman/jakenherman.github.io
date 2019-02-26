---
layout: post
title:  "Creating Firebase Cloud Functions in TypeScript"
excerpt: "Before JavaScript classes were introduced, object methods and constructors were handled a bit differently."
comments : true
date:   2019-02-25 07:00:00 -0600
categories: [TypeScript]
---

Firebase is awesome. Let's just start with that. Super cheap, super easy to set up and use, and loads of functionality offered. That being said, let's look at how to create cloud functions for Firebase in TypeScript.

What are Cloud Functions?
---
Cloud Functions are single-purpose JavaScript functions that are executed in a secure, managed Node.js environment. Basically, they allow you to create a mobile backend without having to deal with the hassle of managing servers. *But wait, this says single-purpose **JavaScript** functions, not TypeScript*. Yeah, that's no big deal - TypeScript is just a JavaScript superset that transcompiles to JavaScript, so we can use it! The cool thing about cloud functions is that they take one command to push to the Firebase servers. After that, Cloud Functions automatically scales up computing resources to match the usage patterns of your app. You never worry about SSH credentials, server configuration, provisioning new servers, or decommissioning old ones. 

Let's Get Started
---
Assuming you already have a Firebase account created with an App on it (if you don't already, it's super easy to create one, so I won't go through it for the purposes of this post), open up a new terminal, navigate to whatever directory you want your firebase cloud functions to live in (or create a new one [`mkdir cloud-functions`]) and type `firebase login`. If you get an error that firebase isn't a recognized cmdlet or something of that nature, just run `npm install -g firebase`. If you had to run the install command, either restart your terminal, or if you are using Powershell or MS Command Line just run `refreshenv` and run the `firebase login` again. You'll be directed to your web browser to log in to your Firebase console. Login, come back to your terminal and run `firebase init`. You'll get a prompt saying "You're about to initialize a Firebase project in this directory: <Your_Directory_Name> Are you ready to proceed?" Type `Y` to proceed, and you'll be greeted with 5 options : Database, Firestore, Functions, Hosting, and Storage. We can look at some of the other selections in another blog post if anyone is interested (leave a comment), but for now we just want functions. Press the down button on your keyboard until you get to `Functions`, then press "Space" on your keyboard to make the selection, and hit "Enter". Now you'll be prompted to select the project you want to create cloud functions for. If you don't already have one, you can create a new project from this window, or select one of the projects you already have. The next question will be whether you want to use JavaScript or TypeScript, which we're obviously going to take TypeScript, so select that. The next option is totally up to you - it asks if you want to use TSLint to catch probable bugs and style enforcement. My view on TSLint is that it can only help, it certainly can't hurt, and I would use it 9 times out of 10. Once you select your TSLint option, a few `.json` files and your `index.ts` file will be created, giving you the following project structure:

{% highlight javascript %}
myproject
 +- functions/  
      |
      +- package.json  # npm pkg file
      |
      +- tsconfig.json
      |
      +- tslint.json # Optional - if you opted out of tslint, this wont be here
      |
      +- src/     # Directory containing TypeScript source
      |   |
      |   +- index.ts  # main source file for your Cloud Functions code
      |
      +- lib/
          |
          +- index.js  # Built/transpiled JavaScript code
          |
          +- index.js.map # Source map for debugging
{% endhighlight %}

You'll be prompted with 1 final question - Do you want to install dependencies with npm now? Type `Y`, as we'll need to install those dependencies eventually, so it might as well be now!

Write & Deploy
---
Once your firebase project has been initialized, open it up in your code editor of choice and look at the default TypeScript code. It's commented out, but it shows you a good example of a helloWorld cloud function, shown below:

{% highlight TypeScript %}
import * as functions from 'firebase-functions';

export const helloWorld = functions.https.onRequest((request, response) => {
 response.send("Hello from Firebase!");
});

{% endhighlight %}

Uncomment that out, and let's send it up to our project. Note that this is how you create functions. If you want a function that will add two numbers, you can do that like so:

{% highlight TypeScript %}
export const addNumbers = functions.https.onRequest((request, response) => {
  response.send(Number(request.query.a) + Number(request.query.b));
});
{% endhighlight %}

Now, let's send these up to the firebase app. Open up your terminal and type `firebase deploy`. Once they're deployed, you can see them in the "Cloud Functions" section of your Firebase console. Then you can call them from your browswer or ping them however you prefer. Cloud functions are super flexible and I would highly recommend trying them out.