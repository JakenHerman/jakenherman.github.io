---
layout: post
title:  "Tying Python’s tkinter Radiobuttons together for single selection allowance"
excerpt: "I have set up some Radiobuttons in Tkinter (Python 3). These are btOrange and btPurple. I need to make sure that only one of them can be selected at a time. How can I do this?"
comments : true
date:   2019-02-12 18:39:39 -0600
categories: [Python]
---

I have set up some Radiobuttons in Tkinter (Python 3). These are `btOrange` and `btPurple`. I need to make sure that only one of them can be selected at a time. How can I do this? Well, let’s first look at the basic setup for tkinter radiobuttons without them being mutually exclusive:

{% highlight Python %}
from tkinter import *

class MyPaint:

    color = "Black"

    def __init__(self):
        window = Tk()


        self.canvas = Canvas(window, width = 750, height = 500, bg = "white")
        self.canvas.pack()

        colorFrame = Frame(window)
        colorFrame.pack()

        btOrange = Radiobutton(colorFrame, text = "Orange", bg = "Orange", command = self.setColor("Orange"))
        btPurple = Radiobutton(colorFrame, text = "Purple", bg = "Purple", command = self.setColor("Purple"))

{% endhighlight %}


This doesn’t work because we haven’t set up a variable that the Radiobuttons route to. Let’s look at the TkDocs documentation for tkinter radiobuttons:

variable : A variable linked to the radiobutton; when the variable is changed, the radiobutton will reflect the new value, while if the user selects the radiobutton, the variable’s value will be updated. If the variable has not been initialized, the radiobutton is shown in an indeterminate state, which usually implies that a choice has not yet been made (and that a default choice is inappropriate).
{: .notice}

We see that we can add in a variable parameter into our `btOrange` and `btPurple` initializations.

That could look something like this:

{% highlight Python %}

self.colorVar = StringVar()
btOrange = Radiobutton(..., variable=self.colorVar, value="Orange")
btPurple = Radiobutton(..., variable=self.colorVar, value="Purple")

{% endhighlight %}

In this case, `self.colorVar` will be automatically set to whichever radio button is selected.