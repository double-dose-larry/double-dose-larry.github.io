---
layout: post
published: false
title: Developing EYE+ pt. 2
---
## EYE+ part 2

for ramblings on part one go [here](https://double-dose-larry.github.io/2020-01-27-developing-eye/)

In the previous post we established that our first round of thinking about measure batter's eye, or ability to identify the pitch and location, wasn't adequate. We need to break down the scoring system on a situational basis. I'm going to do this going from simple -> complicated and see where we end up

### first thing is to identify the elements

My idea is to build a sort of value matrix that we can use to identify how a pitch should be scored. There could be three values for each situation. The batter took an action that denotes a "good" batter's eye, a neutral result and a decision that counts as "poor". Of course, I'm making all of this up.


Just of the top of my head I can imagine a 2D value matrix between count and batter action like so:
1 is good eye, 0 is neutral, -1 is bad eye

#### pitch is in the zone ####

| count   | in zone   |   edge pitches|   well outside|
|:--------|:----------|--------------:|--------------:|
| 0-0     | 0         |  0            | 0            |
| 0-1     | 0         |  0            | 0            |
| 0-2     | 0         |  -1           | 0            |
| 1-0     | 0         |  0            | 0            |
| 1-1     | 0         |  0            | 0            |
| 1-2     | 0         |  -1           | 0            |
| 2-0     | 0         |  0            | 0            |
| 2-1     | 0         |  0            | 0            |
| 2-2     | 1         |  -1           | 0            |
| 3-0     | 0         |  0            | 0            |
| 3-1     | 0         |  0            | 0            |
| 3-2     | 1         |  -1           | 0            |

so basically when pitch is in the strikezone and the batter has two strikes, if they don't offer at the pitch, I count it as bad eye. All other situations are neutral.
