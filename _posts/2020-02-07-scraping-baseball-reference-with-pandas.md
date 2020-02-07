---
layout: post
published: true
title: Scraping baseball-reference with pandas
date: '2020-02-07'
---

I've had lot fun with baseball-reference.com. I mean *A LOT*. I once spent 3 hours looking through the starting line ups of the 1928 season. For a baseball nerd, it's so much fun. You can download all the tables as Excel files and really have some fun.

But I've graduted from excel and now do most of my analysis, as bad as it is, with Python and the pandas library. One of the most underated features of pandas, I think, is it's ability to hoover up a table into a DataFrame. This ability applies to almost any format that you would find structured data in: CSV, SQL, Excel, xml and, most important for us, html. It makes things so much easier than the typcical BeautifulSoup -> table -> do a bunch of work to create a DataFrame of yester-year. I mean it's the same workflow, it's just mostly automated by pandas. 

One issue with scraping from the wild wild web is that the 'table', that holds the structured data, is not always transparant in the DOM structure of the website. This is where pandas would stumble. But, fear not dear reader, for I have the secret to making scraping baseball-reference.com, and really any sports-reference.com page, a breeze. 

Every table on baseball-refernce.com comes with a few options hidden in the 'Share & more' menu. In this dropdown menu you'll see a few options, including export options to CSV and Excel. But that's not what we are looking for. What we are looking for is the 'Embed this Table' option.

![Share & more dropdown](https://imgur.com/a/ibyiAbh)

Once you click on that you'll get a popup with some html code to embed the table in on a website some where. I've never actually used that for it's intended purpose... wait... this is a website, let's see what it does.

<script type="text/javascript" src="https://widgets.sports-reference.com/wg.fcgi?css=1&site=br&url=%2Fleagues%2FMLB%2F1928.shtml&div=div_expanded_standings_overall"></script>

Neat.

Anyway, getting back on topic. In that bit of html code there is a src attribute that points to a special version of that chart you are looking at. The very neat part about all of this is that that version of the table is very pandas friendly. It will get you the neatest version of that table, without all the fuss and muss of scraping the entire webpage.

Here's how we do it.

```python
import pandas as pd

# grab the url from the src attribute of the embed code from baseball-reference.com
url = "https://widgets.sports-reference.com/wg.fcgi?css=1&site=br&url=%2Fleagues%2FMLB%2F1928.shtml&div=div_expanded_standings_overall"

# grab the data and put it in a DataFrame
df = pd.read_html(url)[0]
```

Booya! here is what it looks like:

[!scraped data](https://imgur.com/a/qTMt0w1)

Beautiful, isn't it.

So there's a couple things that we still need to do and explain.

Notice the index of 0 in the code here:

```python
# grab the data and put it in a DataFrame
df = pd.read_html(url)[0]
```

What pandas.read_html() does is return a list of all the tables that it could find on the website. The beauty of this approach is that there will always be one table from the embed url, the table we want. That means we can package it into a function and not ever worry about it.

Another thing that you may notice is tht the last row of the DataFrame is wierd. That's because the last row is exactly as it appears on the website. It's great for presenting the viewer with an additional bit of information, but it's deterimental if you're trying to do an analysis on the data, but it's an easy thing to fix. 

Here's how:

```python
# grab the data and put it in a DataFrame
df = pd.read_html(url)[0].dropna()
```

And now we have a prestine DataFrame to work with. We can do some fun analysis and plotting or whatever. For example:

```python
df.sort_values("Luck").plot(x="Tm", y="Luck", kind="barh", legend=None, figsize=(10,10), title="Team Luck in 1928")
```

![Luck Chart](https://imgur.com/a/ufTTegr)


Join me next time when we expand on this concept and attempt scrape 10 years of Tampa Bays line ups with  10 lines of code.