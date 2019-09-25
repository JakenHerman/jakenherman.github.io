---
layout: post
title:  "Setting up Automatic React Application Deploys on Heroku Dynos"
excerpt: "Building a Community Market listing React App for MLB The Show 19 [Part 1]"
comments : true
date:   2019-09-24 20:39:39 -0600
categories: [React, JavaScript, API]
---

Per the sub-title, this is "Part 1". In this series, we're going to build out a community market listing react application for MLB The Show 19 and set up an automatic pipeline to build and deploy our React application from a GitHub repository to a Heroku Dyno. In this post we will scaffold out the react app and get the automatic deployment set up for Heroku, which will prepare ourselves to create the components necessary to list out all listings for MLB The Show 19's Community Market. Why MLB The Show 19? Because... it's *baseball*. If you're not familiar with MLB The Show 19 - it's a baseball video game for PlayStation 4 and it has a community market that allows players to list baseball cards, stadiums, and equipment that other players can buy to use for their team. In this project, we will only build out listings for baseball cards (i.e. players), not stadiums or equipment or anything else. If that is something that interests you, I would highly recommend you extend the application to meet your needs.

The first thing we need to do to get started is to create a GitHub repository to have source control over our application and to have a place to store our code. To do this, go to GitHub.com and create a GitHub repository. Then, to get that repository on your local machine, use either a git GUI program or just use the command line interface and run the following:

{% highlight shell %}
git clone https://www.github.com/<path_to_your_project>
{% endhighlight %}

Then, change directories to your GitHub repository by running:

{% highlight shell %}
cd <your_project_name>
{% endhighlight %}

The next thing we need to do is actually get into the meat and potatoes of the application. We need to build something to put on our newly created GitHub repository. To do this, we need to create a new react application. Open up your command line interface and run the command:

{% highlight shell %}
 npx create-react-app mlb-the-show-community-market-listings
 {% endhighlight %}

 This command will install `react`, `react-dom`,  `react-scripts`, and a few other packages that you will find useful. `create-react-app` is a facebook-supported way to create single-page React applications that many folks in the front-end community use. Unlike next, razzle, and a few other popular server-side rendering frameworks, CRA renders content on the client-side, which could have some downsides in performance, but we are not necessarily worried about that for the purposes of this project.

 Now that your application has been created, let's just leave it at that - we will make code changes in the next post. For right now, we're going to check in the project as-is. So, via some git GUI or command line, commit your changes and push your code to your GitHub repository:

{% highlight shell %}
git add .
git commit -m 'initial commit'
git push origin master
{% endhighlight %}

We want our Heroku Dyno to rebuild our application every time a change is made to the `master` branch on our GitHub repository. But before we set this up, we need to create a Heroku Pipeline! Assuming you already have a Heroku application created, navigate to dashboard.heroku.com/apps, then select "New" followed by "Create new pipeline". In the pipeline name input field, type 'mlb-the-show-cm-listings'. Next, set yourself to be the Pipeline owner, then in the area that says "Connect to GitHub", connect your GitHub account to this Heroku pipeline. Once you've connected your GitHub account, select the GitHub repository we created earlier in the post by searching for the repository name, then press the "Connect" button. Once your GitHub repository has been connected, press the "Create pipeline" button.

Once your pipeline has been created, you will see a page that has three "steps": Review Apps, Staging, Production. In the card underneath the "Staging" step, press the "Add app..." button, followed by the purple "Create new app..." button. In the app name, you'll have to think of something on your own, as heroku app names must be unique. Once you've decided on a name, press the "Create app" button to finalize the app creation.

Now under your "Staging" area, the card you see will contain your newly created app. Click on your app name under the "Staging" area to open the Heroku app, then go to "Settings". Scroll down until you see the section labeled "Buildpacks". Press the purple "Add buildpack" button, then select the `nodejs` buildpack from the list of officially supported buildpacks, then press "Save changes".

Next, navigate away from "Settings" by clicking on the "Deploy" tab. Scroll down until you reach the section labeled "Automatic deploys". Press the gray "Enable Automatic Deploys" button. You will see the text change to read

> Automatic deploys from `master` are enabled

Now, we just need to trigger the deploy. Let's make a change to our project and commit/push the changes so our Heroku deploy will be triggered. 

Open the `src` folder of your React app we created earlier in this post, and in `App.js`, change the line that says:

{% highlight html %}
<p>
  Edit <code>src/App.js</code> and save to reload.
</p>
{% endhighlight %}

to 

{% highlight html %}
<h1>Hello Heroku!</h1>
{% endhighlight %}

Next, via some git GUI or command line, commit your changes and push your code to your GitHub repository:

{% highlight shell %}
git add .
git commit -m 'trigger heroku deploy'
git push origin master
{% endhighlight %}

Now navigate to your heroku app's activity page to see if a build was triggered: `https://dashboard.heroku.com/apps/<your_app_name>/activity`. If the build failed due to a message similar to this

> A Node.js app on Heroku requires a 'package.json' at the root of the directory structure.

then all you need to do is make sure your github repository doesn't consist of another folder containing your react app rather than the repository containing the react app itself.

Another common issue is having an outdated Yarn lockfile, so if you still get a build failure, go to your command line (within your react app directory), and run the following commands:

{% highlight shell %}
yarn install
git add yarn.lock
git commit -m 'updated yarn lockfile'
git push origin master
{% endhighlight %}

If you don't have a failure, you will see "Build in progress..." for a while, which will then change to "Build succeeded". Once you have a "Build succeed", a new activity will be created on your activity feed and it will say "Deployed `SHA_OF_YOUR_COMMIT`". 

So that's great - we've set up a Heroku dyno to automatically deploy our react application when a change is made. The only problem is... where does it deploy to? Navigate away from the "Activity" tab and go to "Settings" again. Scroll down until you see "Domains and certificates". In the "Domain" section, you will see a line like:

> Your app can be found at <some_link_to_your_app>

Navigating to that domain address will show your application. Keep in mind, you can add a custom domain at any point.

Fantastic - now we've got a react app automatically deploying to a Heroku dyno, now we just need that react app to do something cool! In the next post, we'll begin creating the React components necessary to view the Community Market listings.