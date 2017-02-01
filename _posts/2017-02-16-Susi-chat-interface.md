---
layout: post
title: First sprint: Susi chat interface
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-16
category: Google Summer of Code
tags: [sample post]
imagefeature: cover1.jpg
comments: true
share: true
---

This blog post aims at sharing the details on how Susi got it’s custom interface. Susi is well trained with proper rules and sufficient data. But it’s lacking a makeover which can attract people to chat with her. So we give her that custom makeover as a chat interface with starter functionalities. We used a particular technology stack which was believed would make the chat process much simpler and flexible.

Handlebars – Why only handlebars? This templating framework helps you to reproduce the chat bubbles without much hassle. Two script blocks with embedded handlebar expressions will do it all. This ensures less front end code without any break in the bubbles template.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

This above template is for displaying the user’s message from the send DOM.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

This above template is used for binding the Susi’s response into the chat bubble. Every time the request is triggered when the user send’s out a query that is the chat message. For example Hi Susi and Susi responses back saying Hello!. So the response is triggered when the user types in the message and Susi queries using the following URL.

*http://loklak.org/api/susi.json?q=Hi Susi*

That is how the Template is being embedded into the interface. Along with that Susi is given a separate avatar or artwork and here is one.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

JQuery – We used JQuery for handling the requests and constantly query the Susi API for the answers. This handles the calls very swiftly and the response time is very quick.

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

In the above code snippet the request is being handled and the response is queried accordingly for the answer. For example, this is the sample JSON

![searchVsAggregate]({{ site.url }}/images/about/searchVsAggregate_1.png)

The above JSON is the response when we type “Hello” into Susi’s chat interface. We track down to expression for the actual answer to be provided.

*data.answers[0].actions[0].expression*

The chat interface also provides other requirements like having keyboard events, scroll events, etc. This chat interface code can be viewed here at asksusi. This is still under development and further enhancements would be to port the telegram UI into it’s functionality.

