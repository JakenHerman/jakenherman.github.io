---
layout: post
title:  "Introduction to the Singleton pattern in C#"
excerpt: "
One of the most known, popular patterns in software engineering is the singleton pattern. What is a singleton? A singleton is a class that is written in such a way that it only allows a single instance of itself to be created, and usually has an access method to obtain the instance. You may choose to use a singleton, for example, if your program has some kind of shared resource like an in-memory cache."
comments : true
date:   2019-02-10 18:39:39 -0600
categories: [C#, Computer Science, Software Engineering, Design Patterns]
---

One of the most known, popular patterns in software engineering is the singleton pattern. What is a singleton? A singleton is a class that is written in such a way that it only allows a single instance of itself to be created, and usually has an access method to obtain the instance. You may choose to use a singleton, for example, if your program has some kind of shared resource like an in-memory cache.

So, again, let’s quickly go over the intent of a singleton before we attempt to implement it. We need to insure that only one instance of the class is instantiated, and we need to provide a global point of access to the object.

Ready? Let’s go. I’ll put the implementation below, and describe why it works and what it is doing after that.

{% highlight C# %}
public class Singleton
{
    private static readonly Singleton instance = new Singleton();
    private Singleton()
    {
        //do constructor stuff here.
    }
    public static Singleton getInstance()
    {
        return this.instance;
    }
}
{% endhighlight %}

So as you can tell, our Singleton class has a class property instance of type… Singleton. That’s right, the singleton class definition includes a property of itself. This variable is the only place in your entire program that will have the text “new Singleton();” unless, of course, it’s in a comment. (Can’t get me on a technicality now, folks.😎).

The Singleton class will also contain a private constructor. Not many class definitions contain a private constructor, however, because we only want to ensure that one instance of our Singleton class is instantiated, we hide our constructor to outside classes.

The final element to the Singleton class is the “getInstance()” method. This method simply returns the instance variable on the Singleton class that instantiated it.

That’s all there is to it, folks. A thread-safe implementation of the singleton pattern in C#. Thanks for reading.