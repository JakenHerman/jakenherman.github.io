---
layout: post
title:  "Perfectly Balanced Strings"
excerpt: "Given a string containing only the characters x and y, find whether there are the same number of xs and ys."
comments : true
date:   2019-02-06 18:39:39 -0600
categories: [C#, Java, Programming Challenge]
---

This is rightfully classified as an easy challenge, so it should take no time to complete. When I first saw it, I immediately thought “Great,I’ll just use C# and a single LINQ statement and call it done”, but then I figured it would be more fun if I also tried to replicate my solution in Java.

First, the text:

> Given a string containing only the characters x and y, find whether there are the same number of xs and ys.
>
> `balanced("xxxyyy") => true`
>
> `balanced("yyyxxx") => true`
>
> `balanced("xxxyyyy") => false`
>
> `balanced("yyxyxxyxxyyyyxxxyxyx") => true`
>
> `balanced("xyxxxxyyyxyxxyxxyy") => false`
>
> `balanced("") => true`
>
> `balanced("x") => false`


See? Easy. So let’s start with the obvious — the C# LINQ statement solution.

{% highlight C# %}
    return input.ToCharArray().Where(x => x == 'x').Count() == input.Where(x => x == 'y').Count();
{% endhighlight %}

So this takes our string `input`, converts it to a character array and then sets up a conditional return `x==y` where `x` = the number of characters in our new character array input that are "x", and the `y` = the number of characters in our new character array input that are "y". This will obviously work even if there are letters or numbers in the input that are not x or y, they will simply be ignored.

Next, the admittedly more clunky Java version:

{% highlight Java %}
public static boolean balanced(String input)
{
    int x = 0;
    int y = 0;
    for(char ch: input.toCharArray())
    {
        x += Character.toLowerCase(ch) == 'x' ? 1 : 0;
        y += Character.toLowerCase(ch) == 'y' ? 1 : 0;

    }

    return x == y;
}
{% endhighlight %}

This does something similar, however, we set up `x` and `y` as integer parameters and then loop through each character in the input string. If the character `ch` is “x”, then our `x` variable gets incremented by 1. If it is not "x", it does not get incremented. Likewise, our `y` variable gets incremented by 1 if the character `ch` is “y”, otherwise, it remains the same.

If you’re a Java-guru, I’m sure this looks like a mess to you — but it is a quick and dirty solution. Comment your best Java solution below if you’d like to join in on the challenge.