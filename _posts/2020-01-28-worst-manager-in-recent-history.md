---
layout: post
published: false
title: Worst Manager in Recent History
---

I was reading [Big Data Baseball](https://www.amazon.com/Big-Data-Baseball-Miracles-20-Year/dp/1250094259/ref=sr_1_2?keywords=big+data+baseball&qid=1580244869&sr=8-2) and the author was waxing poetic about Clint Hurdle. This got me to thinking, who's the worst manager in baseball.

I mean it's easy to figure if you look at the win-loss record and [rank the managers by winning percentage](https://www.sportingnews.com/us/mlb/list/worst-baseball-managers-30-years-rankings-ratings/1mrnr1antoi991rgyqmqfaqmv5/15), but I'm not talking about that. In a lot of ways the win-loss records is a reflection of the entire organizations. A team that's put on the field are the responsibility of the front office. The player's need to perform in order to beat the other teams. Listen, if you reserect Joe McCarthy, he ain't taking the Marlins to the World Series. 

So how much of the win-loss record is affected by the manager?

One way that I can think of is to build a regression model based on the team's talent. One way to measure team's talent is to look at WAR at each position. This way we'll build a model and train it on historical data and use it to predict the amount of wins a team *should* have had. The difference between that and the actual record will be attributed to the manager.

Look, dear reader, I know that this is probably wrong on many fundamental levels, but this is just for fun so don't ruin it, okay?

First we get the data. We can get it from [here]