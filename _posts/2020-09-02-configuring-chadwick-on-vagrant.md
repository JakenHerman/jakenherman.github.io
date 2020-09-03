---
layout: post
title:  "Configuring + Installing Chadwick for Parsing Retrosheet Data"
excerpt: "With VirtualBox + Vagrant Installed, the last thing we need before parsing Retrosheet data is to have Chadwick configured and installed."
comments : true
date:   2020-09-02 12:07:00 -0600
categories: [MLB, Data Science, Chadwick, Retrosheet]
---

![Henry Chadwick]({{ site.url }}/img/chadwick.jpg)

---

This post assumes you've set up VirtualBox & Vagrant. If you have not completed this step, follow the steps outlined in my previous blog post: https://www.jakenherman.com/articles/2020-08/virtualbox-vagrant-setup.

The first thing we're going to do is open up our terminal and run `cd baseball`, which is the directory we created in the previous post.

After than, we need to get the `.tar.gz` that contains the Chadwick software installer and configuration files. To download this, go to the chadwickbureau GitHub page, the Chadwick repository, and navigate to the "Releases" page. Here's a quick link to take you there directly: https://github.com/chadwickbureau/chadwick/releases

Take the latest release in the `.tar.gz` format, and move that file into your baseball directory. Once the tar file is in your baseball directory, in your terminal run the command `vagrant up`, followed by `vagrant ssh` . 

Your terminal instance will now be running on your VirtualBox virtual machine. What we need to do now is move the tar file we downloaded earlier into the `usr/local/src directory` (this file will currently be sitting in `~/vagrant`). We'll first navigate to the directory we're moving the file into by running the command `cd /usr/local/src`, then run the command below to copy the Chadwick tar file into the current directory (keep in mind, my file's version number is 0.8.1, but yours may be different - update your command accordingly):

![Copy and Unpack the Chadwick Tar File]({{ site.url }}/img/copy_chadwick_to_src.png)

Now that Chadwick has been copied and unpacked, we need to configure the software and complete the installation. To do this, run the `configure` file that you can see in the `chadwick-0.8.1` directory when you run `ls`, then `make` to compile, `make install` to install the software to our virtual machine, and `ldconfig` to make sure the program can link to the libraries it needs:

![Configure, Make, Install, and Link the new Chadwick Files]({{ site.url }}/img/configure_chadwick.png)

To test that Chadwick was properly installed, run the `cwevent` command, and you should get the following output:

![cwevent should succesfully fail (what a strange sentance)]({{ site.url }}/img/cwevent_test.png)

While this is technically an error, it means the installation was a success. `cwevent` is a command that Chadwick uses to parse Retrosheet event files, and since we've not yet provided one - we get this warning.

I hope this was helpful to you in your quest to begin working with Chadwick and Retrosheet. In the next post, we'll download our first few Retrosheet files and begin exploring.