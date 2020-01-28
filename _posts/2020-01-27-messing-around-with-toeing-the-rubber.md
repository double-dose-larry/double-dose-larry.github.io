---
layout: post
published: true
title: Oliver Drake and the mound
subtitle: Oliver Drake on the mound
date: '2020-01-27'
---

I was some research into Oliver Drake's nasty splitter and I noticed something in the replays. In some replays Drake was on the extreeeeeme right (from the catcher's perspective) of the rubber. Like look at this, he doesn't even look like he's on it here:

[extreme right](https://sporty-clips.mlb.com/35baefdf-5d49-4691-b891-cfcb25d9cd20.mp4) - @ Houston 8/28/2019

and sometimes he was pretty much in the center

[more towards the center of the rubber](https://sporty-clips.mlb.com/c2fb72c1-a255-468e-baa8-16955d51107b.mp4) - Baltimore 7/01/2019

It's plain to the eye that Drake was **purposfuly** positioned differently.

For whatever reason, I've always thought that this never happens. I mean a pitcher changing his position on the mound like that. It's hard enough to throw a baseball where you want it when everything is the same, but then you go and mess with the mechanics of the delivery.

Maybe it's something that happens all the time and we just don't pay attention to it, maybe it happens once a season, where pitchers make adjustments and then stick to the one position that works the best.

Anyway, let's enumerate a few quesitons to explore:

* How can we identify if a pitcher has moved his starting position on the mound?
* Can we track the change in position to a per game/per pitch/per ab level?
* Is the pitcher more successful in one position or another?

For now I'll just work with Oliver Drake's 2019 season because I know he has at some points changed his starting pitch position on the mound. In another post I'll try to expand this to the rest of the league.

Some descriptive stats to set the context:

|     |   4-Seam Fastball |   Split Finger |
|:----|------------------:|---------------:|
| Home |               182 |            282 |
| Away |               197 |            277 |

Nice and simple pitch mix, perfect for exploration.


Luckily Statcast has as a measurement that we can use for this, called [realease_pos_x](https://baseballsavant.mlb.com/csv-docs#release_pos_x) which is

> Horizontal Release Position of the ball measured in feet from the catcher's perspective.

This measure is 0 if the release point is exactly down the middle from the center of the plate extended to the pitcher mound. 

It's nice that Drake throws only to pitches, because we can plot them over each other and not get too cluttered.

If we bin the relase_pos_x into a few buckets and plot the frequencies we start to see a picture.

[img](link to pitch freq chart)

Drake throws most of his pitches from the extreeme right side of the mound(from the catcher's perspective). That's kinda interesting right. I wonder how he compares to other right handers; is he an outlier, or is this something that's pretty common (something for another analysis). I know from watching my boy that he's like a lefty in disguise. His splitter, which can be so nasty, has very similar action as a lefty throwing a slider. 

[gif](link to nasty Drake splitter gif)

What we also see is that there's a different distribution between his fastball release and his spiltter release. I'm assuming this has something to do with his arm slot being different for each type of pitch. For the sake of simplicity, we'll just one pitch, his splitter, and drill down on that.

Let's just ignore the fact that the pitcher's arm slot can change with each pitch and assume that Drake delivers his splitter exactly the same every time. Obviously this is a real consideration, but I'm not trying to write a paper here, I'm just fucking around.

Okay, now that we have set up our universe, let's take a look at the outliers and see if they can tell us anything about anything.


Let's plot the pitches again, but with a box plot. A box plot is useful here because it shows the distribution and individual outliers. Again we can see that Drake operates on the right-most side of the mound, but we can also see that there is a handful of outliers.

![All of 2019](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%202019.jpg)

Do the same thing, but for each month:

## May

![May](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%20month%20of%20May.jpg)

## June

![June](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%20month%20of%20Jun.jpg)

## July

![July](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%20month%20of%20Jul.jpg)

## August

![August](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%20month%20of%20Aug.jpg)

## September

![September](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Boxplot%20of%20Oliver%20Drake%20release%20position%20x%20for%20month%20of%20Sep.jpg)

Lol, one of these is not like the other. Now we're getting somewhere. July seems to have the most outliers. let's take a look at the batters faced in July


|name_last   | name_first   | stands   | avg  release_pos_x |
|:------------|:-------------|:--------|----------------:|
| mancini     | trey         | R       |        0.06108  |
| urshela     | gio          | R       |        0.2055   |
| lemahieu    | dj           | R       |        0.252917 |
| voit        | luke         | R       |        0.35665  |
| torres      | gleyber      | R       |        0.371157 |
| judge       | aaron        | R       |        0.4184   |
| guerrero    | vladimir     | R       |        0.53966  |
| engel       | adam         | R       |        0.71694  |
| rondon      | jose         | R       |        0.732925 |
| grichuk     | randal       | R       |        0.91956  |
| villar      | jonathan     | L       |        1.1683   |
| gurriel     | lourdes      | R       |        1.1932   |
| mckinney    | billy        | L       |        1.38177  |
| smith       | dwight       | L       |        1.38665  |
| santander   | anthony      | L       |        1.46014  |
| gardner     | brett        | L       |        1.52477  |
| holt        | brock        | L       |        1.52984  |
| tauchman    | mike         | L       |        1.64703  |
| gregorius   | didi         | L       |        1.67337  |
| sanchez     | carlos       | L       |        1.70068  |
| bradley     | jackie       | L       |        1.78065  |
| goins       | ryan         | L       |        1.8089   |
| jay         | jon          | L       |        1.82413  |
| garcia      | leury        | L       |        1.8865   |

Notice a pattern? That's right, the right handers!

Plotting this another way confirms it. let's plot the average release_pos_x by month and batter handidness. 

![Left vs Right](https://raw.githubusercontent.com/double-dose-larry/jup_notebooks_baseball/master/2019-01-28-drake/Average%20release%20pos%20x%20by%20Month%20L%20vs%20R.jpg)

And there it is! Oliver Drake toed the rubber differently for righties in July of last year. Clearly he abandoned it quickly, going back to his extreeme right side starting position.

Why? Because it didn't work.

Looking at his [spilts against righties around that time](https://www.fangraphs.com/players/oliver-drake/8823/splits-tool?position=P&splitArr=6&strgroup=month&statgroup=1&startDate=2019-05-26&endDate=2019-09-27&filter=&statType=player&autoPt=true&players=&sort=NaN,1) we see that in the 38 righties faced in Jun he gave up 5 earned runs and 5 walks. Not good, hence the adjustment. Then in the month of July he gave up **6** runs and **5** walks in only **16** righties faced. That's atrocious. I wonder what other tweaks were made after, because he was able to handle righties pretty decently August and on.

What ever it was I hope he continues to develop and work on it because his numbers against lefties are [*elite*](https://www.fangraphs.com/players/oliver-drake/8823/splits-tool?position=P&splitArr=5&strgroup=month&statgroup=1&startDate=2019-05-26&endDate=2019-09-27&filter=&statType=player&autoPt=true&players=&sort=NaN,1) and with the new 3 batter minimum rule going into effect in 2020, I'm looking for Drake to be a goto weapon for Cash during the season.

I'm not sure how much enjoyement you got out of this journey, dear reader, but for me this was delightful. For one, I learned that pitchers change positions per at bat. I knew anecodetly, pitchers talk about making adjustments through out the season all the time, I just never seen one so clearly laid out as this. Also super interesting is that this strategy was abandoned after a few tries.
