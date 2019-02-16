---
layout: post
title: Knuth’s up-arrow notation
excerpt: "Let's look at a recursive function to calculate Knuth's up-arrow notation."
date: 2018-08-04 18:39:39 -0600
categories: [Mathematics, Programming Challenge, C#]
comments: true
---
Donald Knuth’s up-arrow notation is based on the fact that multiplication can be viewed as *iterated addition* and exponentiation as *iterated multiplication*. A single arrow just represents exponentiation. Multiple arrows means iterating the operation associated with one less arrow. So if you have 2 arrows, that’s *iterated exponentiation*, or **tetration**. If you have 3 arrows, that’s *iterated tetration*, or **pentation**. So on and so forth.

The general definition of the notation is as follows:
![Knuth Notation]({{ site.url }}/img/Knuth.png)

Because I love recursion and the definition uses recursion (and because reddit’s Daily Programmer Challenge #365 told me to), I decided to give this a shot in C#. It’s actually really easy to do in a few lines of code.

{% highlight C# %}
/* Knuth's Up Arrow Notaion */
static double up(double a, double b, double n)
{
    if (n == 1) return Math.Pow(a, b);
    else if (n>=1&&b==0)return 1;
    else return up(a, up(a, (b-1), n), n-1);
}
{% endhighlight %}