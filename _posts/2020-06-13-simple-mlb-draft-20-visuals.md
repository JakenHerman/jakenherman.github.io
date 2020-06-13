---
layout: post
title:  "MLB Draft '20 By The Numbers"
excerpt: "A few simple visuals breaking down the MLB Draft '20 Rounds 1-5"
comments : true
date:   2020-06-11 12:07:00 -0600
categories: [MLB, JavaScript, Data Visualization]
---

With no baseball being played so far in 2020, there hasn't been anything incredibly interesting to analyze or look at besides historical data (in the MLB at least). On June 10th and June 11th, however, we finally got our first bit of new MLB information to play around with - the draft. I've taken data from Rounds 1-5 and compiled them into some (hopefully) interesting visuals.

<h1>Picks by State</h1>

Let's start with a simple question. What state produced the most sought after baseball talent this year? California. The values used for the visual below may not reflect where a player was born and raised, rather it is the location of the high school or college the player was drafted from. This also excludes Owen Caissie and David Calabrese of Ontario, Canada.

<iframe
  src="https://codesandbox.io/embed/mlb-20-draft-picks-by-state-9h3b5?fontsize=11&hidenavigation=1&module=%2Fsrc%2Findex.js&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="mlb-20-draft-picks-by-state"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-autoplay allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>


<h1>Picks by Position</h1>

Next, let's look at draft picks by position. This includes every single pick - all 159 of them. As you can see in the chart below, pitchers were definitely shown some love while first basemen lagged behind (Although the #1 pick Spencer Torkelson played 1B, his primary position was marked as OF on MLB. This is likely the case for many utility players).

<iframe
  src="https://codesandbox.io/embed/misty-sun-z3g7e?fontsize=11&hidenavigation=1&module=%2Fsrc%2Findex.js&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="mlb-20-draft-picks-by-position"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-autoplay allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

So who <strong>didn't</strong> take any pitchers? Only <em>three</em> teams! The Detroit Tigers, Tampba Bay Rays, and Milwaukee Brewers.

<div style="display: flex; max-width: 800px; margin-left: auto; margin-right: auto; margin-top: 45px; margin-bottom: 45px;">
  <img src="{{ site.url }}/img/MLBLogos/tigers.png" alt="Detroit Tigers Logo" height="100" />
  <img src="{{ site.url }}/img/MLBLogos/rays.png" alt="Tampa Bay Rays Logo" height="100"  />
  <img src="{{ site.url }}/img/MLBLogos/brewers.png" alt="Milwaukee Brewers Logo" height="100" />
</div>

With all of these pitchers being picked, let's see how the top 5 picks compare to one another using WHIP, ERA, BB/9, HR/9, and H/9. Not that these metrics alone tell you the sole offensive value of a pitcher, I just chose them for fun. (FYI for non-baseball fans, for all of these metrics a lower number is preferable).

<h1>Top 5 Pitcher Metrics Heatmap</h1>
<iframe
  src="https://codesandbox.io/embed/mlb-draft-20-top-5-pitchers-metrics-heatmap-kwx6p?fontsize=11&hidenavigation=1&module=%2Fsrc%2Findex.js&theme=dark"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
  title="mlb-draft-20-top-5-pitchers-metrics-heatmap"
  allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr; xr-spatial-tracking"
  sandbox="allow-autoplay allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

I'd love to do many more draft visualizations and maybe even dip into some KBO numbers, but for now I'm going to call it a night! Thanks for stopping by.