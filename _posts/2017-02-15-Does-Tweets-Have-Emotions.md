---
layout: post
title: DOES TWEETS HAVE EMOTIONS?
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-15
category: Google Summer of Code
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

Tweets do intend some kind of emotion when they are tweeted. It can be happiness, sad, anticipation etc. Loklak does such classification and gives you the categorization of the tweet along with the probability of it being correct.

![Tweets]({{ site.url }}/images/about/tweetsEmotions.png)

The sentiment analysis is one such tool which uses the classification provided by the Loklak Search API from the field called “classifier_emotion”. It displays the other metrics like the languages “classifier_language” in which the tweet is being tweeted along with the emotions. These results are visualized with the help of flash cards along with pie charts.

![Tweets]({{ site.url }}/images/about/tweetsEmotions_2.png)

![Tweets]({{ site.url }}/images/about/tweetsEmotions_3.png)

This has a clean display of the results which shows the recent 10 tweets being tweeted using the hashtag mentioned. One should simply enter the hashtag in to the search box for the results. The following image shows part of the search API results(JSONObject).

![Tweets]({{ site.url }}/images/about/tweetsEmotions_4.png)

I used the above field names”classifier_emotion”, “classifier_language” to display the results. I have used Highcharts to display piecharts.

The internal churning and analysis of the data is happening in the following folder structure [org->loklak->tools->bayes]. Where an abstract Classifier class is being implemented in which the Bayes classifier implements a naive Bayes approach to classifying a given set of features:


{% highlight css %}
classify(feat1,…,featN) = argmax(P(cat)*PROD(P(featI|cat)
{% endhighlight %}


