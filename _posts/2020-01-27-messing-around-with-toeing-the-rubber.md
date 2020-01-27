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

This measure is 0 if the release point is exactly down the middle from the center of the plate extended to the pitcher mound. Let's just ignore the fact that the pitcher's arm slot can change with each pitch, or for different types of pitches and assume that Drake delivers the ball exactly the same every time. Obviously this is a real consideration, but I'm not trying to write a paper here, I'm just fucking around.

Anyway, now that we have a measure to go of off, let's see how those 900 or so pitches thrown in 2019 shape up when it comes to "release_pos_x". In the below chart I grouped the release_pos_x into 5 bins to see how many pitches were thrown from each relative position

