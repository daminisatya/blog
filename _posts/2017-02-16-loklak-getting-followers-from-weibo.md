---
layout: post
title: Loklak getting followers from weibo
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-16
category: Google Summer of Code
tags: [sample post]
imagefeature: cover10.jpg
comments: true
share: true
---


Like twitter loklak has started to scrap the Weibo data. Sina Weibo is a Chinese microblogging (weibo) website. Akin to a hybrid of Twitter and Facebook, it is one of the most popular sites in China, in use by well over 30% of Internet users, with a market penetration similar to the United States’ Twitter.

I have started to scrape the user’s bio page which looks something like this.

![weibo]({{ site.url }}/images/about/weibo_1.png)

The above image is a user’s profile on Weibo. It has two frames of profile, one is a user’s bio which is similar to facebook’s bio page. The second one is completely similar to the twitter’s format. So i scraped the user’s followers details which was in the form of table. Using JSoup we can scrap tables easily.

![weibo]({{ site.url }}/images/about/weibo_2.png)

![weibo]({{ site.url }}/images/about/weibo_3.png)

This is how the table on the profile page got scraped and can get the followers data from Weibo. Stay tuned for more scraping updates.

