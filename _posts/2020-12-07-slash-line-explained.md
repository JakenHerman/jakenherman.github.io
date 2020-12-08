---
layout: post
title:  "What is a 'Slash Line'?"
excerpt: "Unpacking one of baseball's most common terms."
comments : true
date:   2020-12-06 12:07:00 -0600
categories: [MLB, Baseball]
---

The "Slash Line" is a term that is often used in discussion about the offensive value of a player, and is sometimes displayed on broadcasts when a player is coming up to bat, but what is it? The slash line is a collection of three statistics:

  - A player's batting average (AVG)
  - A player's on-base percentage (OBP)
  - A player's slugging percentage (SLG)

The combination of these three player statistics combined with a forward slash is where the name “slash line” comes from. Sometimes, the slash line is referred to as the triple-slash line.

It’s not uncommon to hear someone say “[Some player] slashed .215/.300/.367 in the 2020 season”. This just means that player *produced* a slash line with a .215 batting average, a .300 OBP, and a .367 SLG.

Why is the slash line so popular? Because summing up a player’s offensive contributions to a team in a single statistic is generally a difficult thing to do, the slash line provides a quick way to see not only how often a player gets a hit but how often that player gets a hit, draws a walk, or gets hit by a pitch in his at-bats. To take it even one step further, because SLG is part of the slash line, it also tells us how often the player gets a hit that results in extra bases. It’s not a perfect summary of a player, but it’s easily digestible even for non-baseball fans, which is likely why it's so popular. If broadcasts started showing more complex stats, it may be off-putting to the casual fan.

So how are the three stats calculated?

**AVG**: This one’s the easiest. You just take the total number of hits a player achieved (H) and divide it by the number of at-bats (AB) that player has had. It’s literally just the rate of hits per at bat. You can deduce pretty quickly why this statistic alone is horrible for valuing a player’s offensive output. It does not take walks or HBP into account, and it doesn’t put any extra weight on more difficult hit outcomes like home runs, triples, or doubles.

![AVG Formula]({{ site.url }}/img/avg_calculation.png)

**OBP**: This one gets a bit more complicated, but not much. This time, we get to incorporate walks (BB, which just means Base on Balls), the batter being hit by pitch (HBP), and sacrifice flies (SF). To calculate a player’s on-base percentage, add the total number of hits (H), walks (BB), and hit-by-pitches (HBP) as the numerator. For the denominator, add the total number of at-bats (AB), walks (BB), hit-by-pitches (HBP), and sacrifice fly balls (SF):

![OBP Formula]({{ site.url }}/img/obp_calculation.png)

**SLG**: Now we get to incorporate some power. SLG is a player’s slugging percentage: how often do they hit the ball hard (draw more than just a single)? This stat actually puts weights on different hit outcomes depending on the number of bases earned by that hit. To calculate SLG, you simply take the Total Bases earned per At Bat (TB) and divide it by the total number of at-bats (AB). To get the Total Bases earned per At Bat, weight each outcome by the number of bases it earned. So for a player’s singles (1B), you would take 1 * 1B, where 1B is the total number of singles he drew. Take that number and add 2 * 2B where 2B is the total number of doubles he achieved. Do the same thing for triples with 3 * 3B, and home runs with 4 * HR. In summary, calculate a player’s SLG with:

![SLG Formula]({{ site.url }}/img/slg_calculation.png)

Again, the slash line (or triple-slash line) is *not* a great indicator of offensive value, but it is commonly used in broadcasts and amongst casual baseball fans, so it's worth looking at what it means and how the values are calculated.