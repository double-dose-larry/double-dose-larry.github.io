---
layout: post
published: true
title: Scrapping baseball-reference.com with pandas pt. 2
---

[In the last installment](https://double-dose-larry.github.io/2020-02-07-scraping-baseball-reference-with-pandas/) we went over how to grab clean data from baseball-reference.com with, essentially, one line of code. Now, let's expand on that concept and see how we can use pandas to and Python to do some heavy-duty scraping. For this exapmle we'll scrape the game logs of my favorite team, the Tampa Bay Rays. The data table for each season is located on the "Schedule & Results" page for that season. For example here is the url for the page that contains the 2019 season game logs:

https://www.baseball-reference.com/teams/TBR/2019-schedule-scores.shtml

As you can see, there is a structure to the url that we'll use to our advantage. While we won't use this url, we'll be using the embed url that we learned about in the [previous post](), the two urls are similar and it's much clearer to the human eye to see the structure here. Basically, if we want to grab the data from any other year, we'll just need to change the '2019' in the url to the year that we want. 

Before we put down some code, let's go grab the embed url that we'll be working with.

![drop-down menu](https://i.imgur.com/PyQ0LeG.png)

![embed table url](https://i.imgur.com/bCBMmjQ.png)


Now that we have the url, let's write a bit of code to test out if pandas can read this table properly.

```python
## imports
import pandas as pd

## set our url, notice where the '2019' appears here
url = "https://widgets.sports-reference.com/wg.fcgi?css=1&site=br&url=%2Fteams%2FTBR%2F2019-schedule-scores.shtml&div=div_team_schedule"

## display in an jupyter notebook
display(pd.read_html(url)[0])
```

![results](https://i.imgur.com/Xk9hTgH.png)

Okay! Not bad, but there are a few issues that we need to deal with

### There are extraneous rows that repeat the header.

There are a few times the header row is repeated. That's great when displaying the data to a person, to make sure they know what column they're looking at, but not great for us. It's easy to fix though; all we have to do is filter out the rows that have the same value as one of the headers, like so:

```python
pd.read_html(url)[0].query('Tm != "Tm"')
```

### There are some Unamed type columns.

If you look at the table on the website, you can see that the column containing the link to the boxscore and the column that designates an away game (with an @) aren't named. pandas helpfully names these for us as 'Unnamed: 2' and 'Unnamed: 4'. Now we don't need the boxscore column, so we can drop that, but we might want to hold on to the 'home or away' column. Here's how I would do it:

```python
pd.read_html(url)[0].query('Tm != "Tm"').drop('Unnamed: 2', axis=1).rename(columns={'Unnamed: 4' : 'H/A'})
```

### Fix Datatypes

One additional thing to consider here is the data types of each column. pandas generally does a good job of recognizing when columns are supposed to be numbers or dates instead of strings, but in our case, it doesn't. I suspect that the additional header columns that we end up dropping. We want the numerical columns, like R and RA, to be numbers so that we can do math with them. There are several ways to approach this problem, including using [astype](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.astype.html#pandas.DataFrame.astype) and [convert_dtypes](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.convert_dtypes.html?highlight=dtypes#pandas.DataFrame.convert_dtypes), but I'm going to share with you my favorite way, that works almost every time as expected, for me anyway.

The approach is to use a pandas function called [to_numeric](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.to_numeric.html) that smartly converts strings to numbers. What we are going to do is [apply](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.apply.html) to_numeric across our entire data frame. The issue is that to_numeric need to have an additional parameter: errors="ignore", otherwise it will raise an error every time it runs into a string that can't be converted. apply doesn't let you pass parameters along with the function, so we need to "pre-load" that parameter using `partial` from the `functools` library. If this sounds like mumbo jumbo to you, don't worry, all you have to do is copy the code and run it. It should work pretty much every time.

```python
pd.read_html(url)[0].query('Tm != "Tm"').drop('Unnamed: 2', axis=1).rename(columns={'Unnamed: 4' : 'H/A'}).apply(partial(pd.to_numeric, errors='ignore'))
```

Now we have a prestine data frame off all the game logs for our Tampa Bay Rays 2019 season scraped, in one line of code, no less.

Before we go on, let's do something quick and fun with this.

```python
df["H/A"] = df["H/A"].fillna("H")
df.groupby(["Gm#","H/A"]).Attendance.sum().unstack().plot(kind="area", figsize=(20,10), rot=0, title="TB Attendance 2019 Home vs Away")
```

![home vs away attendance](https://i.imgur.com/CYOebe7.png)

Hmm... on second thought this wasn't fun at all

Anyway, let's proceed. Now that we have a way to pull down data for one year, let's package it into a function and see how we can pull down multiple years of game logs

Since we're going to be spanning different years, let's have our function take the year as a parameter. It's going to look something like this:

```python
def tb_game_logs(year):
	print("getting year", year)
    url = f"https://widgets.sports-reference.com/wg.fcgi?css=1&site=br&url=%2Fteams%2FTBR%2F{year}-schedule-scores.shtml&div=div_team_schedule"
    df = pd.read_html(url)[0].query('Tm != "Tm"').drop('Unnamed: 2', axis=1).rename(columns={'Unnamed: 4' : 'H/A'}).apply(partial(pd.to_numeric, errors='ignore'))
    df["year"] = year
    return df
```

Only a couple of things to expand on here. For one, I'm using an f string to stick the year into the url. You can use format or % if you're more comfortable with that. Point is that we're changing the url to pull the data we want. Luckily, it's very predictable with baseball-reference.com urls and we can easily do so. The other thing is adding the year to the dataframe. There's no indication of the year in the actual data, and we're going to need to know this when we're putting multiple datasets together. Also I like getting a little bit of feedback when looping, the print statement let's me keep track of the progress.


From here the idea is to run a loop through multiple years, bringing back a dataframe for each year, and then finally stiching them all together at the end. 

The last part is easy with pandas. Since we know that every dataframe will have exactly the same structure we can use [concat](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html) to stick them together. And since we need a list of dataframes for concat to work, a list comprehension is the most pythonic way to approach this.

Here's the code:

```python
df = pd.concat([ tb_game_logs(yr) for yr in range(2009,2020)])
```

The resulting dataframe, df, has all the game log data for Tampa Bay Rays seasons 2009 through 2019. That's 1783 games. On my machine it took 28 seconds to run.

Here is what the final code looks like:
```python
## imports
import pandas as pd
from functools import partial

## define scraping function
def tb_game_logs(year):
    print("getting year", year)
    url = f"https://widgets.sports-reference.com/wg.fcgi?css=1&site=br&url=%2Fteams%2FTBR%2F{year}-schedule-scores.shtml&div=div_team_schedule"
    df = pd.read_html(url)[0].query('Tm != "Tm"').drop('Unnamed: 2', axis=1).rename(columns={'Unnamed: 4' : 'H/A'}).apply(partial(pd.to_numeric, errors='ignore'))
    df["year"] = year
    return df

## get data for range of years
df = pd.concat([ tb_game_logs(yr) for yr in range(2009,2020)])
```

That's it. Without the comments, that's 9 lines of code, not too shabby.


