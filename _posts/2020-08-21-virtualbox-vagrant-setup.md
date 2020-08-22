---
layout: post
title:  "Setting up VirtualBox+Vagrant"
excerpt: "Setting up the VirtualBox + Vagrant Environment"
comments : true
date:   2020-08-21 12:07:00 -0600
categories: [MLB, Environment Setup, Vagrant]
---
Setting up VirtualBox and Vagrant is not only a breeze, but it's also free. This combo is great for simple projects, much like the project we're working on in this series (should you choose to finish this full series) - parsing Retrosheet baseball data using Chadwick in order to create useful R data frames for visualization.

---
Keep in mind throughout this post that your download+setup process may vary slightly, but the main process will remain similar enough to follow.

# Step 1: Download and Install VirtualBox
Navigate to the VirtualBox download page here: https://www.virtualbox.org/wiki/Downloads, and select the download that is appropriate for your current operating system.

![VirtualBox Download Page]({{ site.url }}/img/VirtualBoxDownload.png)


Run your installer and complete the standard installation process you follow for any other software.

> MacOS Users: An issue may occur where your installation is being blocked by your Security & Privacy settings. If this occurs, do the following:

![Security Privacy Window Error]({{ site.url }}/img/Security-Privacy-Window.png)

 - Open `System Preferences`
 - Go to `Security & Privacy`
 - There will be a message that says `System software from developer "Oracle America, Inc." was blocked from loading.`
 - Click the lock icon in the bottom left of the window & enter your password
 - Click the `Allow` button

---

# Step 2: Download & Install Vagrant
Navigate to the Vagrant download page here: https://www.vagrantup.com/downloads, and select the download that is appropriate for your current operating system.

![Vagrant Download Page]({{ site.url }}/img/VagrantDownload.png)

Run your installer and complete the standard installation process you follow for any other software.

---

# Step 3: Set up Directory and Initialize Vagrant Box
Now that we have VirtualBox and Vagrant installed, we need to set up a directory to use the two together. Keep in mind, we'll never explicitly open the VirtualBox application, we only downloaded and installed it so Vagrant would be able to use it in the background.


Open up your terminal, make a new directory (in this example I named mine baseball), then initialize a Vagrant box of your choice (boxes listed here: https://app.vagrantup.com/boxes/search). In this example, I'm using ubuntu/trusty64:

![Initialize Vagrant Box]({{ site.url }}/img/VagrantInit.png)

The `vagrant init ...` command could take up to an hour to run, so grab a cup of joe ☕, it may be a while!
When your initialization is complete, you'll notice a file called `Vagrantfile` in your baseball directory. As described by the Vagrant website:

> The primary function of the Vagrantfile is to describe the type of machine required for a project, and how to configure and provision these machines.

---

# Step 4: Run Vagrant + SSH In
Once your Vagrant box has been initialized, the next step is easy - just run vagrant up to spool up your VirtualBox background process and SSH in:

![SSH Into Vagrant Box]({{ site.url }}/img/VagrantUp.png)

You'll now be in your virtual machine! Keep in mind when using this that if you create a file in the directory `/vagrant`, the files will be added to your non-virtual `baseball` directory.

Thanks for reading. Check back in the next post and we'll get Chadwick downloaded and configured so we can begin playing around with Retrosheet data!