---
layout: post
title: Search vs Aggregations
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-09
category: Google Summer of Code
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

The search aggregations also know as facets(Field aggregations) are often ignored while using the Search API provided by Loklak. This post aims at clearing up the difference and bring out the clear usage. This extends the previous blog, titled “Know who tweeted the most!” where we discussed about the Search API. Using the same example, the results were viewed using the search aggregations. The following two pictures illustrates the difference.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_2.png)

The above results are achieved by scraping the aggregation field called mentions, which contains the list of user names who mentioned the search hashtag in their tweets. The result is from the one billion tweets(~1,377,367,341) which Loklak had scraped and indexed. The following screenshots show the JSON object of the search aggregations.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_3.png)

The above search metadata object shows some important fields which can alter the result. The count is set to zero and the cache is disabled so that the aggregations do not consider the remote search results.The query fields shows the constraints on which the query must be performed. It shows the hashtag for which it must query. Since the search aggregations are going to query the whole Loklak index(over one billion tweets) we can limit the result payload by giving time constraints such as “since” and “until” fields. We can even limit the result display by mentioning a value to the limit field. This helps you to form a search query which gives you a much accurate result. The following is a sample query where you can check out the JSON result. Edit the “q” variable to your search requirement and the time fields too.

{% highlight css %}
http://loklak.org/api/search.json?q=loklak since:2016-01-01 until:2016-03-01&source=cache&count=0&fields=mentions,hashtags
{% endhighlight %}

The following shows the aggregations field and the benefits you can get out of it.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_4.png)

The aggregations field consists of the hashtags and the mentions. The mentions contains all user names denoted by a ‘@’-prefix from the message, which is being listed without the leading ‘@’. The hashtags contains all hashtags appearing in the message, without the leading ‘#’. You have more fields which you can mention in the query according to your need such as limit, source, timezoneOffset, minified etc. For more info on the search aggregations visit the docs page.

You can even visit to the app “knowTheDiff” which guides you through the difference with step by step intro.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_5.png)

The app is still under construction and needs to get more fields into the picture, but can try out the basic difference. Here are some sample queries where you can try out.

{% highlight css %}
http://loklak.org/api/search.json?q=loklak since:2015-04-05_23:10until:2015-04-05_23:20&source=cache&count=0&fields=created_at&timezoneOffset=-120
{% endhighlight %}

{% highlight css %}
http://loklak.org/api/search.json?q=loklak since:2015-04-01 until:2015-04-06&source=cache&count=0&fields=mentions,hashtags&limit=6
{% endhighlight %}
