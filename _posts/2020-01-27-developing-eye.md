---
layout: post
published: true
title: Developing EYE+
subtitle: EYE+
image: >-
  https://imgc.allpostersimages.com/img/print/posters/close-up-of-a-baseball-player-swinging-a-baseball-bat_a-L-4021139-4990875.jpg
---
## Thoughts on EYE+

What makes a batter have a good batter eye? 

Batter's eye is something that, and I'm totally making this up, is a batter's ability to spot the rotation and trajectory of a pitch and be able to take the appropriate action. This is related, but distictly different than the batter's ability to hit the ball. That's a totally different skill. 

So what happens when someone has a "good" batter's eye? That batter will potentially be able to draw a lot of walks, assuming that they use their "eye" to take close but non-strike pitches.

To take an extreeme example, Joey Votto, anecodetly, has good batter's eye. He walks a ton and he's an all time great in OBP. Any measurement of "eye" should have him in the top. 


so how do we measure this ability?

My first thought was to measure how well the batter handle pitches just outside the edges of the strike zone. A simple measure of "good" result versus all chances at the edge. with a good result being:

* a ball or a called strike
* a well hit ball
* a foul if there are two strikes in the count

Of course this would be a "plus" stat so then I took the leauge average "eye" ratio, which happened to be .688, and normalized it.

Here is the leaderboard:


| name_first   | name_last   |   edge_chances |   good_result |      eye |   eye_plus |   rank |
|:-------------|:------------|---------------:|--------------:|---------:|-----------:|-------:|
| logan        | forsythe    |            364 |           312 | 0.857143 |    130.512 |      1 |
| andrew       | mccutchen   |            300 |           255 | 0.85     |    129.424 |      2 |
| alex         | bregman     |            708 |           593 | 0.837571 |    127.531 |      3 |
| greg         | garcia      |            408 |           341 | 0.835784 |    127.259 |      4 |
| cavan        | biggio      |            441 |           367 | 0.8322   |    126.714 |      5 |
| alex         | avila       |            184 |           153 | 0.831522 |    126.61  |      6 |
| robbie       | grossman    |            463 |           381 | 0.822894 |    125.297 |      7 |
| zack         | collins     |            121 |            99 | 0.818182 |    124.579 |      8 |
| mike         | trout       |            596 |           486 | 0.815436 |    124.161 |      9 |
| myles        | straw       |            144 |           116 | 0.805556 |    122.657 |     10 |
| dan          | vogelbach   |            630 |           506 | 0.803175 |    122.294 |     11 |
| david        | fletcher    |            622 |           499 | 0.802251 |    122.153 |     12 |
| eric         | sogard      |            395 |           315 | 0.797468 |    121.425 |     13 |
| curt         | casali      |            231 |           184 | 0.796537 |    121.283 |     14 |
| rhys         | hoskins     |            780 |           621 | 0.796154 |    121.225 |     15 |

not great


but not awful either.

After this exercise I realized two major problems with this measure:

1. a good "eye" also means that a batter doesn't let the good pitches go by unnecessarily
2. the "well hit ball" and "foul" criteria are measures of results, not intent.

Let's think about the second problem first.

I want this metric to be a measure of ability to react to the ball. In other words, a measure of wether or not the batter takes the correct actions at the appropriate times. Taking a step back, the batter has really, a binary choice with each pitch. Swing or don't swing. Theoretically, if a batter recognizes that a pitch will end up outside of the strike zone, they won't offer at the pitch. The "ball or called strike" criteria is a good measure of that ability. In other words, the batter doesn't offer at what should have been called a ball. Whether or not the pitch is called a ball shouldn't matter, because it's not the batter's fault if it it's not. Of course this is an oversimplification. If the ump is calling a wide zone that day, it will most certainly effect the batter's actions. In a sense we can't objectively measure if a pitch should be offered at, because we don't know what the strikezone is like for that game. 

But for the sake of practicality, we have to assume that we know what the strike zone is and assume that the ump is calling the game to the predefine strike zone. I think ulitmately when taking data over a seasons worth of pitches, we can assume that this is true. 

Let's think about the first problem, second.

My man Logan Forsythe has the best eye in baseball. Does that sound right to you? Me, neither. Nothing against Logan, but I would hardly call him the best in baseball for anything. What he does do ... um ... well, is not swing. He doesn't swing at practically anything, so it make sense that he lays off of more pitches on the edges as well.

what this boils down to, I think, is the fact that we need to measure all chances, and assign a "good eye" value to the actions taken by the batter. The batter who doesn't offer at a pitch down the middle should be an unfavorable result when measuring "eye". "Well, what about if it's 3-0 and the team is down by 2?" you ask. And to that I say, "You're correct!". Ranking an action taken as favorable or unfavorable in terms of batter's eye is very situational. It heavily depends on, and I'm making this up,  on the count and the score and to some degree the inning. 

Ok things are now getting quite complicated, but not impossible. Join me in the next post to think about  how we can properly take all these things into account...