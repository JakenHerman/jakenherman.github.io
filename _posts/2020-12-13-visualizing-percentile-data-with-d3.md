---
layout: post
title:  "Visualizing Percentile Data with d3"
excerpt: "Recreating Baseball Savant's Percentile Ranking Visualization"
comments : true
date:   2020-12-13 12:07:00 -0600
categories: [MLB, Baseball, JavaScript, Data Visualization, d3]
---

On Baseball Savant ([https://baseballsavant.mlb.com](https://baseballsavant.mlb.com)), they have these great visualizations for displaying percentile rankings. Basically, out of the population of MLB athletes, where does a player stand in comparison for a given statistic? In the photograph below, I've snipped a few stats (Exit Velocity, xBA, K%, and Sprint Speed). We're going to replicate this visualization using d3 today. (For the record, this is Daniel Vogelbach (MIL) vs. 2020 season data)

![Baseball Savant's Percentile Ranking Visualization]({{ site.url }}/img/baseball_savant_percentiles.png)

First, I'll assume you have some familiarity with d3 as well as some familiarity with what *slight* modifications will be necessary between traditional d3 and the code we're going to write today, which is d3 formatted for Observable ([https://observablehq.com](https://observablehq.com/@jakenherman)). Let's load in d3:

{% highlight javascript %}
d3 = require("d3@5", "d3-array@2", "d3-color@2", "d3-scale-chromatic@2")
{% endhighlight %}
<iframe width="100%" height="109" frameborder="0"
  src="https://observablehq.com/embed/@jakenherman/visualizing-percentile-data?cell=d3"></iframe>

Next, we need to set up a helper function to get our cx values. Because the width of our canvas is going to be 150 pixels but percentiles are ranged 0-100, we have to do some calculation for the actual x values:
{% highlight javascript %}
getX = (percentile) => {
    return (150*percentile) / 100;
};
{% endhighlight %}

Now, let's add our data. We're going to format our data as a collection of objects that hold information about the statistic label, the value of the statistic (this will be our cx value, so we're going to utilize the `getX()` function we've just written), and the y-value of where the statistic will be displayed:
{% highlight javascript %}
percentileData = [
  { label: 'Exit Velocity', cx: getX(63), cy: 30 },     
  { label: 'xBA', cx: getX(29), cy: 60 },     
  { label: 'K%', cx: getX(40), cy: 90 },     
  { label: 'Sprint Speed', cx: getX(5), cy: 120 }
];
{% endhighlight %}

We're cookin' with gas, now! Let's define our SVG:

{% highlight javascript %}
svg = d3.create('svg')
    .attr('width', 170)
    .attr('height', 150);
{% endhighlight %}

The first thing we're going to add to our new `svg` is the horizontal lines in which each percentile ranking will be displayed. This is pretty simple to do, because the x1 and x2 values will be 0 - 160 (we just want to go straight across our svg which has a width of 170), and the y1 and y2 values will be the same (and they're the `cy` key in our `percentileData` object):

{% highlight javascript %}
  const lines = svg.selectAll('line')
                  .data(percentileData)
                  .enter()
                  .append('line')
                    .style('stroke', 'rgb(155, 155, 155)')
                    .style('stroke-width', 2)
                    .attr('x1', 10)
                    .attr('x2', 160)
                    .attr('y1', d => d.cy)
                    .attr('y2', d => d.cy);
{% endhighlight %}

![Lines]({{ site.url }}/img/PercentileRankingPost/lines.svg)

The horizontal lines are a good start, but they don't look the same as Baseball Savant's horizontal lines do... yet! Baseball savant has circular decorators on their lines at the 0, 50, and 100th percentile positions. This makes it easy to identify how far off the measure of center a player is. Let's add these now:

{% highlight javascript %}
lineDecorators = [
    { cx: getX(0), cy: 30 },     
    { cx: getX(50), cy: 30 },     
    { cx: getX(100), cy: 30 },
    { cx: getX(0), cy: 60 },     
    { cx: getX(50), cy: 60 },     
    { cx: getX(100), cy: 60 },     
    { cx: getX(0), cy: 90 },     
    { cx: getX(50), cy: 90 },     
    { cx: getX(100), cy: 90 },     
    { cx: getX(0), cy: 120 },     
    { cx: getX(50), cy: 120 },     
    { cx: getX(100), cy: 120 }  
  ];

 decorators = svg.selectAll('#decor')
                   .data(lineDecorators)
                   .enter()
                   .append('circle')
                      .attr('id', 'decor')
                        .attr('cx', d => d.cx + 10 )
                        .attr('cy', d => d.cy)
                      .attr('r', 3)
                      .attr('fill', 'rgb(155, 155, 155)');
{% endhighlight %}

![Decorators]({{ site.url }}/img/PercentileRankingPost/decorators.svg)

Much better. Now, the fun part. Let's add our circles that indicate where a player ranks in relation to other players in the MLB. To do this, we're going to need to do some more math for the label positioning, but we're also going to need to make use of `d3.interpolateRdBu()`. The value that goes inside of this function (which just colors the circle) is going to be the inverse of what we *actually* want, so we're going to subtract our real value from 1 to get the desired color. Note that we're not actually putting the label on the circle yet, we're just trying to figure out where the label would be positioned on the line so that we can color it appropriately:

{% highlight javascript %}
circles = svg.selectAll('.ranks')
                   .data(percentileData)
                   .enter()
                   .append('circle')
                      .attr('class', 'ranks')
                      .attr('cx', d => d.cx + 10 )
                      .attr('cy', d => d.cy )
                      .attr('r', d => 10)
                      .attr('fill', d => d3.interpolateRdBu(1-(Math.floor((d.cx/150)*100) / 100)))
                      .attr('stroke', 'black');
{% endhighlight %}

![Circles]({{ site.url }}/img/PercentileRankingPost/circles.svg)

Look at that! It's close, but we're still missing labels. Both for the statistic we're showing and for the actual percentile ranking number. Let's do the labels for which statistic we're showing first:

{% highlight javascript %}
statLabels = svg.selectAll('.labels')
                    .data(percentileData)
                    .enter()
                    .append('text')
                        .attr('class', 'labels')
                        .attr('x', 5)
                        .attr('y', d => d.cy - 6)
                        .text(d => d.label)
                        .attr('font-family', 'sans-serif')
                        .attr('font-weight', 'bolder')
                        .attr('font-size', '.6rem')
                        .attr('fill', 'black');
{% endhighlight %}

![Stat Labels]({{ site.url }}/img/PercentileRankingPost/statLabels.svg)

This is looking really good. The last step (displaying the percentile ranking number) requires the use of another helper function. Because of the font sizing, we need to tweak our x values a bit before slapping them on our svg:

{% highlight javascript %}
getTextXValue = (x) => {
   const stringLength = Math.floor((x/150)*100).toString().length;
   switch (stringLength) {
    case 1: return x + 7;
    case 2: return x + 4;
    default: return x;
   }
};
{% endhighlight %}

At first it looks like hocus pocus, but you should be able to see why this is an important step. (hint: it's due to the svg size being 170, percentiles ranging from 0-100, and the fact that the values may be 1 digit long, 2 digits long, or 3 digits long.)

Okay, let's finally get our text labels up and running:

{% highlight javascript %}
text = svg.selectAll('.percentRank')
              .data(percentileData)
              .enter()
              .append('text')
                  .attr('class', 'percentRank')
                  .attr('x', d => getTextXValue(d.cx))
                  .attr('y', d => d.cy + 3)
                  .text(d => Math.floor((d.cx/150)*100))
                  .attr('font-weight', 'bolder')
                  .attr('font-size', '.7rem')
                  .attr('fill', d  => (Math.floor((d.cx/150)*100) >= 70 ||
                                       Math.floor((d.cx/150)*100) <= 30)
                        ? 'white' : 'black');
{% endhighlight %}

![Final]({{ site.url }}/img/PercentileRankingPost/final.svg)

Tada! The final product looks great, and it's an easy way to visualize percentile data. I hope you've enjoyed this quick walkthrough. The full observable notebook is available here:
[https://observablehq.com/@jakenherman/visualizing-percentile-data](https://observablehq.com/@jakenherman/visualizing-percentile-data).
