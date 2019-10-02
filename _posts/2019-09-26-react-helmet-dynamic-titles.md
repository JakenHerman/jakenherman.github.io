---
layout: post
title:  "Dynamic HTML Titles in React with NFL's Helmet"
excerpt: "Update HTML document head on the fly with react-helmet"
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

Because we haven't made any modifications to the document title yet, the title within the tab should be "React App" by default. For this simple example, we're going to change the title based on a certain `state` within our `App` component. So, let's modify our functional component `App` to be a class component, and give it a state object that will hold the value we'd like our title to be:

{% highlight React%}
import React from 'react';
import './App.css';

class App extends React.Component {
  
  constructor(props) {
    super(props);
    this.state = {
      titleName: ''
    };
  }

  render () {
    return (
      <div className="App">
        <h1>Hello World</h1>
      </div>
    );
  }
}

export default App;
{% endhighlight %}

Now this will, of course, make no change to the title at this point (after all, we haven't even installed `react-helmet` yet!), but we're just setting up our project so when we get to the `react-helmet` part, it's much more satisfying. What I'd like to do is add an input field that allows the user to type in what they would like the title of the tab to be. So we're going to create an input and in the `onChange` of that input, we're going to update our `state`'s `titleName` key's value to the value within the input, like so:

{% highlight React%}
class App extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      titleName: ''
    };
  }

  changeTitle(ev) {
    this.setState({
      titleName: ev.target.value
    });
  }

  render () {
    return (
      <div className="App">
        <h1>{this.state.titleName}</h1>
        <input onChange={this.changeTitle.bind(this)}></input>
      </div>
    );
  }
}
{% endhighlight %}

As you can see, I threw the `this.state.titleName` in an `<h1>` so we would have quick-and-easy proof that our state is being updated when the input's `onChange` event is fired.

Now, for the fun part. Open up your CLI and run the command:

{% highlight Shell %}
  $ npm i react-helmet

  # or, using Yarn:
  $ yarn add react-helmet
{% endhighlight %}

Now that `react-helmet` has been added to our project, we can add it to our `<App />` component. To do this, we're first going to simply import the component, then just like we would in a typical HTML file, we're going to put the title information at the very top of our `render()` return, only instead of wrapping it in a `<head>` tag, we're going to wrap it in `<Helmet>` tags. And of course, for the `<title>`'s value, we're going to set it to `this.state.titleName`:

{% highlight React%}
import React from 'react';
import { Helmet } from 'react-helmet';

class App extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      titleName: ''
    };
  }

  changeTitle(ev) {
    this.setState({
      titleName: ev.target.value
    });
  }

  render () {
    return (
      <div className="App">
        <Helmet>
          <title>{this.state.titleName}</title>
        </Helmet>
        <input onChange={this.changeTitle.bind(this)}></input>
      </div>
    );
  }
}

export default App;
{% endhighlight %}

Now when changes are made to the input field, you can see the html title changes in the browser tab:
![Dynamic Titles in React]({{ site.url }}/img/dynamic_title.gif)

 > `<Helmet>` can be used on any components, just keep in mind that child components will always override and helmet data passed through their parent components.
 
 Thanks for reading, folks. Hope this taught you something.
