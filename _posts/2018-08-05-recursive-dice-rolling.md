---
layout: post
title:  "A Recursive Dice-Rolling Simulator"
excerpt: "Who needs physical dice for D&D when you have a computer and recursion?"
comments : true
date:   2018-08-05 18:39:39 -0600
categories: [C#]
---

Who needs physical dice for D&D when you have a computer and recursion? I wrote a function that will roll a dice with m sides n times. The input is ndm. So, in order to roll 3d20 or 5d6, all you have to do is call `roll(3, 20, 0)` or `roll(5, 6, 0)`, respectively.

{% highlight C# %}
static int roll(int times, int max, int value)
{
    return times == 0 ? value += new Random().Next(1, max+1) 
                      : value += roll(times-1, max, new Random().Next(1, max+1));
}
{% endhighlight %}

Of course, the function above returns the sum of all of the dice rolls. So, what if we want to list out each individual roll? No problem — I also wrote another function called `bonus_roll` (also recursive) that handles this for us. To roll 3d20 or 5d6, you’ll call `bonus_roll(3, 20, 0, new List())` or `bonus_roll(5, 6, 0, new List())`, respectively.

{% highlight C# %}
static void bonus_roll(int times, int max, int value, List<int> prev_values)
{
    if (times == 0)
    {
        prev_values.Add(new Random().Next(1, max+1));
        prev_values.Reverse();

        int sum = 0;
        foreach(int number in prev_values)
        {
            sum += number;
        }

        Console.Write(string.Format("{0} : ", sum));
        foreach(int number in prev_values)
        {
            if(number != 0)
                Console.Write(string.Format("{0} ", number));
        }
    }
    else
    {
        prev_values.Add(value);
        bonus_roll(times - 1, max, new Random().Next(1, max + 1), prev_values);
    }
}
{% endhighlight %}

This isn’t very succinct or pretty like `roll()` and it is by no means efficient, but it gets the job done and it’s fairly readable.