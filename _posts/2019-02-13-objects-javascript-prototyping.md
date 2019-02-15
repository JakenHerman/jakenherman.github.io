---
layout: post
title:  "Creating Objects in JavaScript using Prototyping"
date:   2019-02-13 18:39:39 -0600
categories: jekyll update
---
JavaScript classes were introduced in ECMAScript 2015, and are primarily syntactical sugar over JavaScript's existing prototype-based inheritance. Let's take a look at what that prototype-based inheritance looks like behind the scenes. 

Let's create a "Reptile" object, that has two properties: type, and age. On that object we'll have setter functions for both properties, and while we're at it, let's say the type will be some custom enumeration as defined below.

{% highlight JavaScript %}
var TypeEnum = {
    CROC_OR_GATOR : 0,
    TURTLE_OR_TORTOISE : 1,
    SNAKE : 2,
    LIZARD : 3,
    NONE : 4,
}
{% endhighlight %}

Let's look at the class implementation of our Reptile class, post ECMAScript 2015, just for reference:
{% highlight JavaScript %}
class Reptile {
  constructor() {
    this.Age = 0;
    this.Type = TypeEnum.NONE;
  }

  // Methods
  setAge(age) {
    this.Age = age;
  }
  
  setType(type) {
    this.Type = type;
  }
}
{% endhighlight %}

This is pretty simple, we have a Reptile class that has an empty constructor function to instantiate. Next, within the class definition we can set two methods: setAge(), and setType(), which do exactly what they sound like they do.

Now, let's look at the prototype implementation - pre ECMAScript 2015 (and what the class definition pretty much does in the background.

{% highlight JavaScript %}
function Reptile() {
    //set defaults
    this.Age = 0;
    this.Type = TypeEnum.NONE;
}

Reptile.prototype = {
    setAge: function(age) {
        this.Age = age;
    },
    setType: function(type)
    {
        this.Type = type;
    }
}

var reptile = new Reptile();

reptile.setAge(15);
reptile.setType(TypeEnum.SNAKE);

//15 2 (Snake)
console.log(reptile.Age + " " + reptile.Type);
{% endhighlight %}

Here we specify what a "Reptile" is. It has an Age property, and a Type property, both being defaulted to a value. Each object in JavaScript has a private property which holds a link to another object called its prototype. This is how we can set up our setAge() and setType() functions. Next, we declare a new Reptile and save it to a variable. JavaScript object constructors are just functions that happen to be called with the new operator. We can then call our functions we set up in the prototype in order to set our reptile instance's Age and Type properties.
After all is said and done, we can then use the console to see our reptile variable's properties were properly set.

This is a very basic example, but I always find it fun to look into how things were done before new improvements in development came around.

{% include advertisements.html %}