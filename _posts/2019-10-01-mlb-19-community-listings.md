---
layout: post
title:  "Fetching and Displaying API Data for MLB The Show 19"
excerpt: "Building a Community Market listing React App for MLB The Show 19 [Part 2]"
comments : true
date:   2019-10-01 20:39:39 -0600
categories: [React, JavaScript, API]
---

Per the sub-title, this is "Part 2". If you didn't read Part 1, I would suggest going back and reading that now. Now that we have a `create-react-app` that automatically deploys to a Heroku Dyno when we push a change to our GitHub repository, it's time to make the app actually do something. Before starting, though, we are going to need to add a few public npm packages, like AG Grid, Semantic UI, and Axios. AG Grid is going to help us display our data retrieved from the API in a nice table format without having to do too much legwork on our own, Semantic UI will help us create a beautiful app with pre-made UI components, and Axios will allow us to make API calls. To add these packages to our application, first `cd` into your project directory, then run the following command:

{% highlight shell %}
npm i --save semantic-ui-react semantic-ui-css axios ag-grid-community ag-grid-react
{% endhighlight %}

Once these packages have all been added, open the project in your favorite code editor. Delete all pre-generated code files within the `src` folder except for `index.js` and `App.js`. In these two files, clear almost everything until your `index.js` file looks like this:

{% highlight react %}
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
{% endhighlight %}
 
And your `App.js` looks like this:

{% highlight react %}
import React from 'react';

function App() {
  return (
    <div className="App">

    </div>
  );
}

export default App;
{% endhighlight %}

The next thing we want to do is make sure all of our Semantic UI stylesheets get imported to our project. To do this, add the following line to `index.js`, just below the `import App from './App';` line:
{% highlight react %}
import 'semantic-ui-css/semantic.min.css'
{% endhighlight %}

Now, the API we will be using to pull community market listings for MLB The Show 19 has a few different filterable options, but for the purposes of this blog, we're going to use the default parameters and just call `https://mlb19.theshownation.com/apis/listings.json`. To see additional capabilities, go to https://mlb19.theshownation.com/api_docs. Before we set up our axios call, we first want to define a state property called `rowData` that will hold our results. To do this, modify `App.js` to look like this:

{% highlight react %}
import React from 'react';

class App extends React.Component {

  constructor (props) {
    super(props);
    this.state = {
      rowData: []
    }
  }

  render() {
    return (
      <div className="App">
  
      </div>
    );
  }
}

export default App;
{% endhighlight %}

Now that our state is set up and ready to be modified once we get data, we can set up an axios call to obtain the data. After the `constructor()` function, but just before the `render()`, add a new function called `getListings()`, and set up an axios inside and set the state's `rowData` to the response of the axios call. Once your component is mounted, make a call to `getListings()`:

{% highlight react %}
 // import * as axios from 'axios' <-- put this in your imports section
  getListings() {
    axios.get('https://cors-anywhere.herokuapp.com/https://mlb19.theshownation.com/apis/listings.json')
    .then((response) => {
      this.setState({
        rowData: response.data
      })
    })
    .catch((err) => {
      console.log(err);
    })
  }

  componentDidMount () {
    this.getListings();
  }
{% endhighlight %}

Now our state will hold the listings data, we just need to display it. To do this, we are going to add a `columnDefs` property to our component's state, then in the `render()` function, we're going to set up AG Grid. So, the new state should look like this in your `constructor()`:

{% highlight react %}
  constructor (props) {
    super(props);
    this.state = {
      columnDefs: [{
        headerName: "Name", field: "name"
      }, {
        headerName: "Best Sell Price", field: "best_sell_price"
      }, {
        headerName: "Best Buy Price", field: "best_buy_price"
      }],
      rowData: []
    }
  }
{% endhighlight %}

Before moving onto our `render()`, let's import necessary AG Grid components and stylesheets:

{% highlight react %}
import { AgGridReact } from 'ag-grid-react';
import 'ag-grid-community/dist/styles/ag-grid.css';
import 'ag-grid-community/dist/styles/ag-theme-balham.css';
{% endhighlight%}

And your new `render()` should look like this:
{% highlight react %}
  render() {
    return (
      <div 
        className="ag-theme-balham"
        style={{ 
        height: '500px', 
        width: '600px' }} 
      >
        <AgGridReact
          columnDefs={this.state.columnDefs}
          rowData={this.state.rowData.listings}>
        </AgGridReact>
      </div>
    );
  }
{% endhighlight %}

Start up your project by running `yarn start`, and behold - you now have live data pulling from MLB The Show 19's community market API. Now, I'd like to center this table and perhaps stick it in a semantic ui segment. To do this, in your imports, add the following:

{% highlight react %}
import { Grid, Segment, Header } from 'semantic-ui-react'
{% endhighlight%}

Then, change your `render()` to include each of the imported components (keep in mind, this is a horrible way of centering AG Grids, but it works for the purposes of this blog):

{% highlight react %}
  render() {
    return (
        <Grid columns={3}>
          <Grid.Row>
            <Grid.Column width={3}></Grid.Column>
            <Grid.Column width={10}>
              <br />
              <Header>MLB The Show 19 Community Market Listings</Header>
              <Segment>
                <div 
                  className="ag-theme-balham"
                  style={{ 
                  height: '500px', 
                  width: '920px' }} 
                >
                  <AgGridReact
                    columnDefs={this.state.columnDefs}
                    rowData={this.state.rowData.listings}>
                  </AgGridReact>
                </div>
              </Segment>
            </Grid.Column>
            <Grid.Column width={3}></Grid.Column>
          </Grid.Row>
        </Grid>
    );
  }
{% endhighlight %}



 
