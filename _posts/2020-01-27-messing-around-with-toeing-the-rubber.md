---
layout: post
published: false
title: Messing around with toeing the rubber
subtitle: Oliver Drake on the mound
date: '2020-01-27'
---
## Pitch starting position

I was some research into Oliver Drake's nasty splitter and I noticed something in the replays. In some replays Drake was on the extreeeeeme right (from the catcher's perspective) of the rubber. Like look at this, he doesn't even look like he's on it here:

[gif of Drake off rubber]

And then on some other pitches, he's pretty much down the center.

[gif of Drake in the middle of the rubber]

This got me wondering, how often does this happen and who does this the most?

For whatever reason, I've always thought that this never happens. I mean a pitcher changing his position on the mound like that. It's hard enough to throw a baseball where you want it when everything is the same, but the you go and mess with the mechanics of the delivery.

Maybe it's something that happens all the time and we just don't pay attention to it, maybe it happens once a season, where pitchers make adjustments and then stick to the one position that works the best.

Anyway, that's a lot of questions so let's enumerate a few to explore:

* How can we identify if a pitcher has moved his starting position on the mound?
* Can we track the change in position to a per game/per pitch/per ab level?
* Is the pitcher more successful in one position or another?

For now I'll just work with Oliver Drake's 2019 season because I know he has at some points changed his starting pitch position on the mound. Later on I'll try to expand this to the rest of the league.

some descriptive stats to set the context:

|     |   4-Seam Fastball |   Split Finger |
|:----|------------------:|---------------:|
| Home |               182 |            282 |
| Away |               197 |            277 |

Nice and simple pitch mix, perfect for exploration.

Here's a couple of examples that we can use to guide us, these I've found from my prior research:

* [extreme right](https://sporty-clips.mlb.com/35baefdf-5d49-4691-b891-cfcb25d9cd20.mp4) - @ Houston 8/28/2019
* [to the left](https://sporty-clips.mlb.com/c2fb72c1-a255-468e-baa8-16955d51107b.mp4) - Baltimore 7/01/2019

Clearly you can see that there's a lot of traveling on the mound.

Luckily Statcast has as a feature for just this, called [realease_position_x](https://baseballsavant.mlb.com/csv-docs#release_pos_x) which is

> Horizontal Release Position of the ball measured in feet from the catcher's perspective.

This measure is 0 if the release point is exactly down the middle from the center of the plate extended to the pitcher mound. 

It's nice that Drake throws only to pitches, because we can plot them over each other and not get too cluttered.

If we bin the relase_pos_x into a few buckets and plot the frequencies we start to see a picture.

[img](link to pitch freq chart)

Drake throws most of his pitches from the extreeme right side of the mound(from the catcher's perspective). That's kinda interesting right. I wonder how he compares to other right handers; is he an outlier, or is this something that's pretty common. I know from watching my boy that he's like a lefty in disguise. His splitter, which can be so nasty, has very similar action as a lefty throwing a slider. 

[gif](link to nasty Drake splitter gif)

What we also see is that there's a different distribution between his fastball release and his spiltter release. I'm assuming this has something to do with his arm slot being different for each type of pitch. For the sake of simplicity, we'll just one pitch, his splitter, and drill down on that.

Let's just ignore the fact that the pitcher's arm slot can change with each pitch and assume that Drake delivers his splitter exactly the same every time. Obviously this is a real consideration, but I'm not trying to write a paper here, I'm just fucking around.

Okay, no that we have set up our universe, let's take a look at the outliers and see if they can tell us anything about anything.

Let's go back to our questions from the beginning and address one by one:

* How can we identify if a pitcher has moved his starting position on the mound?

Well it seems that we can using release_pos_x. Here are the top 3 right most splitters based on that measure:

[gif](link to right most toe)

And here are the top 3 left most splitters:

[gif](link to left most toe)

It's plain to the eye that Drake was **purposfuly** positioned differently.

* Can we track the change in position to a per game/per pitch/per ab level?

Well, we can, because we have the data. Let's plot those splitters again, but with a box plot. A box plot is useful here because it shows the distribution and individual outliers. Again we can see that Drake operates on the right-most side of the mound, but we can also see that there is a handful of outliers.

[img](boxplot)

Do the same thing, but for each month:

[img](boxplot may)

[img](boxplot june)

[img](boxplot july)

[img](boxplot august)

[img](boxplot september)

What's interesting here is that it doesn't appear to be a mid season adjustment, but rather a strategy employed on certain occasions.

* Is the pitcher more successful in one position or another?

Unfortunatley I don't think we can answer this question very well. There are just too few pitches thrown from the "non-normal" starting positon.

For what it's worth here are some stats on those pitches.




