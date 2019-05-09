---
layout: post
title:  "How to Learn a New Programming Language"
excerpt: "The best way to learn any language is to simply just use it."
comments : true
date:   2019-05-09 08:00:00 -0600
categories: [Programming, Learning, Tips and Tricks]
---
The best way to learn **any** language is to simply *just use it*.

With that being said, I often find that new developers just want to learn the newest, flashiest, most "cool" language like Python or some new JavaScript library. This endeavor may be fruitless if you are not first familiar with the underlying concepts and techniques associated with programming in general.

The best advice that I can offer would be to learn algorithms, design patterns, and programming fundamentals. Once you have learned these things, you can write virtually any program in virtually any language.

For example - I do not know how to use the language Ruby. However, I am about to walk you through the popular FizzBuzz program in Ruby by using my knowledge of programming fundamentals (loops, conditionals, operators, io, etc.):

The first thing I need to do is define the problem. This is the first step to writing **any** program. If you don't first know what the problem is, you cannot find a solution to it. The problem is as such: For each number from 1 to 100 I would like to print "Fizz" if the number is divisible by 3, "Buzz" if the number is divisible by 5, or "FizzBuzz" if the number is divisible by both.

The next thing I need to do is check the Ruby documentation for using a "[loop][1]":

    a = 0

    until a > 100 do
      a += 1
    end

Now that I have an `until` loop, I need to check how to do modular arithmetic in Ruby by once again, checking the [documentation][2], as well as checking [how to call `if` statements][3], then applying what I've found, modifying my code as such:

    a = 0

    until a > 100 do

      if a % 3 == 0
        print fizz
      end

      if a % 5 == 0
        print buzz
      end

      a += 1
    end

Lastly, you'll notice I just wrote "print fizz" and "print buzz" in my if statements. Now I need to check [how to write my results][4] via the documentation, and modify my code as such:

    a = 1

    until a > 100 do

      if a % 3 == 0
        print "fizz"
      end

      if a % 5 == 0
        print "buzz"
      end

      a += 1
      puts ""
    end

There we go - my first ruby program has been written. You saw my thought process as well as my methods on finding out *how* to get the program done. Now I can think of a more difficult or complex program, and use the same methods to write it in ruby. In time, just by **using** ruby, I will have learned it.

Also keep in mind that this program is likely not the best way of handling things - there are improvements to be made. That is okay. Nobody will expect you to write perfect code while learning. 

So how do you learn Python or JavaScript or C++ or literally **any other language**? Replace every instance of the word "Ruby" in this answer, and replace it with whichever programming language you want to learn. By the end, you'll have a FizzBuzz program. Then, all you have to do is think of another more complex problem and **just do it.**

  [1]: https://docs.ruby-lang.org/en/2.4.0/syntax/control_expressions_rdoc.html#label-until+Loop
  [2]: http://ruby-doc.org/core-1.9.3/Numeric.html#method-i-modulo
  [3]: https://ruby-doc.org/core-2.3.0/doc/syntax/control_expressions_rdoc.html
  [4]: https://docs.ruby-lang.org/en/2.6.0/IRB/OutputMethod.html
