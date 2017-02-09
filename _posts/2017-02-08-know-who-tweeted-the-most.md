---
layout: post
title: Know Who Tweeted The Most!
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-08
category: Google Summer of Code
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

It is obvious that all of us are curious to find out who is leading! The app, which is called ‘Twitter Leaderboard’ uses the [search API](http://loklak.org/api/search.json) provided by ‘Loklak’. Using the app you can collect the top five tweeters whose tweets contain the mentioned hashtag.

So here is a simple explanation of how [‘Twitter Leaderboard’](http://loklak.org/apps/tweetsleaderboard/) works. I built this app using AngularJS and the search API provided by [Loklak](http://loklak.org/). Primarily, I collected the tweets’ data and parsed it for the required fields.

The leader board needed to have the tweeter’s name along with their tweet count. Also ‘Twitter Leaderboard’ needed to allow its users to search for a tweet based on the hashtag supplied to it in a query. 

I wrote a small controller to make a HTTP request to the Loklak search API, and parse the retrieved object accordingly.  I parsed the required data in the following manner:


{% highlight css %}
data.statuses //The status object containing the requested hashtag.
user = statuses[i].screen_name // Get all the screen names.
counts = {} //Counts object to store the number of tweets count for each name.
After parsing for the required data from the search results, we have to sort the names according to the tweets count.  And here we go the results are pushed to the front end and displayed.
{% endhighlight %}

![twitterLeaderboard]({{ site.url }}/images/about/TwitterLeaderBoard.png)

Another way to improve the search result is by using the Search Aggregations. This feature helps you to get the count results in a better by scaling up the search result. It will help you to count up all the tweets which are indexed(More than a billion tweets). This feature will not consider remote search results. Therefore the remote search is switched off by “source=cache” and the search results are switched off with “count=0”. The request for aggregation is simply hidden in “fields=…” which names the fields where you want to have an aggregation. You can even reduce the result size by restricting your search to certain period of time.

The upgrade to the above app will be provided soon using the Aggregations.

