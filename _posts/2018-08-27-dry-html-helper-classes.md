---
layout: post
title:  "Writing D.R.Y. HTML with .Net Helper Classes"
excerpt: "There have been far too many times I’ve looked at HTML that I’ve written (and that others have written) where I’ve thought to myself “this is terrible.” Up to 100 lines of code all doing the exact same thing over and over again. If you had to make a change in the code, you’d need to do it on every single occurrence of the code block.

Luckily, this can be avoided with HTML .NET Helper classes."
comments : true
date:   2018-08-27 18:39:39 -0600
categories: [HTML, .NET, C#]
---

There have been far too many times I’ve looked at HTML that I’ve written (and that others have written) where I’ve thought to myself “this is terrible.” Up to 100 lines of code all doing the exact same thing over and over again. If you had to make a change in the code, you’d need to do it on every single occurrence of the code block.

Luckily, this can be avoided with HTML .NET Helper classes. In my examples, I’ll be showing you C#, but they can very easily be done in VB.NET in a similar way.

What kind of HTML gets repeated? Any type of HTML that is used to generate reports or documents frequently repeats a header for the page, and a footer for the page. So, let’s look at that type of example. Let’s look at the old way of handling this:

{% highlight html %}
 <div class="page">
  <div class="header-content">
    <h1>Company Name</h1>
    <h2>Company Slogan</h2>
    <p>Name of Document</p>
  </div>
   
   <div class="content">
      CONTENT ON PAGE 1
   </div>
   
  <div class="footer-content">
    <p>Name of Company</p>
    <div class="contact">Company Contact Information</div>
    <p> Page Number 1 </p>
  </div>
</div>

<div class="page">
  <div class="header-content">
    <h1>Company Name</h1>
    <h2>Company Slogan</h2>
    <p>Name of Document</p>
  </div>
   
   <div class="content">
     CONTENT ON PAGE 2
   </div>
   
  <div class="footer-content">
    <p>Name of Company</p>
    <div class="contact">Company Contact Information</div>
    <p> Page Number 2</p>
  </div>
</div>
{% endhighlight %}

In the example above, the headers and footers are the exact same on both pages of the document. If the document is 20 pages long, you’ll end up repeating the same exact HTML 20 times each. That’s not good.

**Why is that not good?** That’s not good because if you need to make a change to, referring to our example, the Company Contact Information, you’d need to do it in 20 different places in your code. It’s likely that you’ll end up with a typo on one of those pages or that you’ll even forget to change one of them. We need to ensure that we can make this change in one spot and have all 20 of the occurrences change with it.

**So how do we do this?** First, we need to write a helper function. Note : My first example will be parameter-less. This will be used for the header, where nothing is going to change across pages:

{% highlight cshtml %}
 @helper HeaderInformation()
{
   <div class="header-content">
    <h1>Company Name</h1>
    <h2>Company Slogan</h2>
    <p>Name of Document</p>
  </div> 
}

<div class="page">
  @HeaderInformation();
   
   <div class="content">
      CONTENT ON PAGE 1
   </div>
   
  <div class="footer-content">
    <p>Name of Company</p>
    <div class="contact">Company Contact Information</div>
    <p> Page Number 1 </p>
  </div>
</div>

<div class="page">
  @HeaderInformation();
   
   <div class="content">
     CONTENT ON PAGE 2
   </div>
   
  <div class="footer-content">
    <p>Name of Company</p>
    <div class="contact">Company Contact Information</div>
    <p> Page Number 2</p>
  </div>
</div>
{% endhighlight %}

As you can see, we’ve created a helper called `HeaderInformation()`. Any time we need to display the header in the HTML, we simply call this function. Now, we need a function for the footer. But we need to change the page number each time. What we’ll do in this case is add a parameter to our helper called pageNumber, and use it within the function, like so:

{% highlight cshtml %}
@helper HeaderInformation()
{
   <div class="header-content">
    <h1>Company Name</h1>
    <h2>Company Slogan</h2>
    <p>Name of Document</p>
  </div> 
}

@helper FooterInformation(int pageNumber)
{
   <div class="footer-content">
    <p>Name of Company</p>
    <div class="contact">Company Contact Information</div>
    <p> Page Number @pageNumber</p>
  </div>
}

<div class="page">
  @HeaderInformation();
   <div class="content">
      CONTENT ON PAGE 1
   </div>
  @FooterInformation(1);
</div>

<div class="page">
  @HeaderInformation();
   <div class="content">
     CONTENT ON PAGE 2
   </div>
  @FooterInformation(2);
</div>
{% endhighlight %}

Here when we call our `FooterInformation()`, we pass in the page number and it gets updated in the HTML. This is obviously a better way of handling repeated HTML because now if we need to change the company contact information, it will get updated on every single page where we call `FooterInformation()`.

There are even more ways you can DRY up this HTML example, but I’ll leave that up to you. The best way to learn is to learn by doing.

Hope you enjoyed. DRY up your code.