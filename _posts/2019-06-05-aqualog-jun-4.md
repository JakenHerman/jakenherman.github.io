---
layout: post
title:  "Aquarium Log - June 4th, 2019"
excerpt: "It's not lookin' too pretty"
comments : true
date:   2019-06-05 08:00:00 -0600
categories: [Fishkeeping, Blog]
---
<img src="{{ site.url }}/img/WaterTests/060419State.jpg" alt="June 4 2019 Aquarium View" width="200"/>

Well, I think it's just best to admit this outright - my aquarium sucks, and my fish are unhappy. My filter broke so my poor aquarium went a while without filtration. As of last night, I officially have replaced the filter, I put on an Aqueon QuietFlow 30 which should work, as my tank is only 36 gallons.

![June 4 2019 Water Test Results]({{ site.url }}/img/WaterTests/060419Results.jpg)

My pH level was expectedly very high. Ammonia seems to be creeping upwards at 0.25ppm, but my nitrite and nitrate levels are ok at 0ppm. My low-range pH value was reading in at about 7.6+ and my high-range pH value was reading in at around 8.2-. My heater seems to be working ok, temperature was reading around 74F.

![Temperature Gauge June 4 2019]({{ site.url }}/img/WaterTests/060419Temp.jpg)


For the past month or two, we have been battling extreme algae presence. Our pleco and snails are not much help as of right now. This could all be due to the busted filter, though. So last night I added 4mL of API AlgaeFix and 20 mL of Seachem Pristine to clear some of the sludge (hopefully). I also added 35mL of Tetra Easy Balance Plus to try to level out the pH in the tank.

We put a new automatic feeder on the back of the tank, which will hopefully help us out as far as not over- or under-feeding the fish. The current state of the tank looks terrible, but I'm hopeful that we can get it cleaned up nicely.

![Auto Feeder]({{ site.url }}/img/Automatic-Feeder.jpg)


I've started working on an aquarium and fishkeeping logging application in Python/Django called AquaMate. It's open sourced, link to GitHub [here](https://github.com/JakenHerman/AquaMate). As of right now, I only have very simple models created, and I know these will change drastically but this is a start:


{% highlight python %}
from django.db import models


class Aquarium(models.Model):
    name = models.CharField(max_length=200)
    created_date = models.DateTimeField('date published')

    def __str__(self):
        return self.name


class Log(models.Model):
    aquarium = models.ForeignKey(Aquarium, on_delete=models.CASCADE)
    created_date = models.DateTimeField('date published')
    ph = models.FloatField(default=0)
    high_range_ph = models.FloatField(default=0)
    ammonia = models.FloatField(default=0)
    nitrite = models.FloatField(default=0)
    nitrate = models.FloatField(default=0)
    notes = models.CharField(max_length=5000)
    
    def __str__(self):
        res = 'ph: ' + str(self.ph) + '\n'
        res = res + 'high_range_ph: ' + str(self.high_range_ph) + '\n'
        res = res + 'ammonia: ' + str(self.ammonia) + '\n'
        res = res + 'nitrite: ' + str(self.nitrite) + '\n'
        res = res + 'nitrate: ' + str(self.nitrate) + '\n'


class Fish(models.Model):
    aquarium = models.ForeignKey(Aquarium, on_delete=models.CASCADE)
    name = models.CharField(max_length=200)
    species = models.CharField(max_length=200, default='')
    quantity = models.IntegerField(default=0)

    def __str__(self):
        return 'species: ' + self.species + '; name: ' + self.name
{% endhighlight %}
