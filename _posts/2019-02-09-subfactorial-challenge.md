---
layout: post
title:  "Subfactorials — Another twist on Factorials"
excerpt: "Let’s look at the subfactorial, which is defined as the derangement of a set of n objects, or a permutation of the elements of a set such that no element will appear in its original position. We’re going to denote it as !n, but note that there is no standard notation agreed upon for the subfactorial function."
comments : true
date:   2019-02-09 18:39:39 -0600
categories: [C#, Programming Challenge, Mathematics]
---
Original problem submitted by [/u/jnazario](https://www.reddit.com/r/u/jnazario) to [/r/dailyprogrammer](https://www.reddit.com/r/dailyprogrammer).

Almost every programmer is familiar with the factorial (n!) of a number, which is, of course, the product of the series from n to 1. An interesting aspect of the factorial operations is that it is also the number of permutations of a set of n objects.

Let’s look at the subfactorial, which is defined as the derangement of a set of n objects, or a permutation of the elements of a set such that no element will appear in its original position. We’re going to denote it as !n, but note that there is no standard notation agreed upon for the subfactorial function.

Some basic definitions:

 * !1 -> 0 because you always have {1}, meaning 1 is always in it’s position.
 * !2 -> 1 because you have {2,1}.
 * !3 -> 2 because you have {2,3,1} and {3,1,2}.

And so forth.

One equation for solving for subfactorials is

`!n = n! / e`

The challenge? Write a subfactorial program. Given an input `n`, we need to calculate the correct value for `n`. Assuming we’re given inputs as one integer per line as the original problem states, the solution is below:

{% highlight C# %}
static int subfactorial(int n)
{
    return (int)Math.Round(factorial(n) / Math.E);
}

static int factorial(int n)
{
    return n == 0 ? 1 : n * factorial(n - 1);
}
{% endhighlight %}

This is a very simple solution. It uses recursion in the factorial function, and uses the factorial function within the subfactorial function to fit our definition stated above.

The factorial function will return an `int` based on whether or not the `int` received is 0. If the `int n` received is 0, it will return 1, otherwise, it will call itself via recursion to multiply the n passed in by the factorial of (n-1). This makes sense, after all, n! = 1*2*3* … * (n-2)*(n-1) * (n).

Once our factorial function finds the factorial of a number `n`,our subfactorial function will take that number, divide it by e, and return the result, leaving us with the subfactorial.