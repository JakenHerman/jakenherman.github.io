---
layout: post
title:  "Dynamic HTML Titles in React with NFL's Helmet"
excerpt: ""
comments : true
date:   2019-09-26 20:39:39 -0600
categories: [React, JavaScript]
---

Using React through `create-react-app` is great, but when we consider that it will create a single-page application, 
we begin to realize that changing properties in the document head of our html file is seemingly not so easy to do - but that
could not be further from the truth. 

`react-helmet` is a reusable React component created by the NFL that can manage all of your changes to the document head, and it could
not be any simpler to use. It supports server-side rendering, and while this blog post is focused solely on changing HTML `title` tags,
`react-helmet` supports all valid head tags: `title`, `base`, `meta`, `link`, `script`, `noscript`, and `style` tags.

Let's quit talking about it and let's get into the code. First, create a new `create-react-app` application (named whatever you want) and open it up in your favorite
text editor (if you don't know how to do this, see the official `create-react-app` [documentation](https://create-react-app.dev/docs/getting-started)

Now that you're in your project, delete the content from the pre-generated  `App.js` file and replace the file with this:

{% highlight React%}
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello World</h1>
    </div>
  );
}

export default App;
{% endhighlight %}
