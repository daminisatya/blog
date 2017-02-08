---
layout: post
title: Know Who Tweeted The Most!
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-08
category: GSoC
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

It is obvious that all of us are curious to find out who is leading! The app, which is called ‘Twitter Leaderboard’ uses the search API provided by ‘Loklak’. Using the app you can collect the top five tweeters whose tweets contain the mentioned hashtag.

So here is a simple explanation of how ‘Twitter Leaderboard’ works. I built this app using AngularJS and the search API provided by Loklak. Primarily, I collected the tweets’ data and parsed it for the required fields.

The leader board needed to have the tweeter’s name along with their tweet count. Also ‘Twitter Leaderboard’ needed to allow its users to search for a tweet based on the hashtag supplied to it in a query. 

I wrote a small controller to make a HTTP request to the Loklak search API, and parse the retrieved object accordingly.  I parsed the required data in the following manner:


{% highlight js %}
data.statuses //The status object containing the requested hashtag.
user = statuses[i].screen_name // Get all the screen names.
counts = {} //Counts object to store the number of tweets count for each name.
After parsing for the required data from the search results, we have to sort the names according to the tweets count.  And here we go the results are pushed to the front end and displayed.
{% endhighlight %}

![twitterLeaderboard]({{ site.url }}/images/about/TwitterLeaderBoard.png)

Another way to improve the search result is by using the Search Aggregations. This feature helps you to get the count results in a better by scaling up the search result. It will help you to count up all the tweets which are indexed(More than a billion tweets). This feature will not consider remote search results. Therefore the remote search is switched off by “source=cache” and the search results are switched off with “count=0”. The request for aggregation is simply hidden in “fields=…” which names the fields where you want to have an aggregation. You can even reduce the result size by restricting your search to certain period of time.

The upgrade to the above app will be provided soon using the Aggregations.


#################################################################################################
Below is just about everything you'll need to style in the theme. Check the source code to see the many embedded elements within paragraphs.

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6


### Body text

Lorem ipsum dolor sit amet, test link adipiscing elit. **This is strong**. Nullam dignissim convallis est. Quisque aliquam.

*This is emphasized*. Donec faucibus. Nunc iaculis suscipit dui. 53 = 125. Water is H<sub>2</sub>O. Nam sit amet sem. Aliquam libero nisi, imperdiet at, tincidunt nec, gravida vehicula, nisl. The New York Times <cite>(That’s a citation)</cite>. <u>Underline</u>. Maecenas ornare tortor. Donec sed tellus eget sapien fringilla nonummy. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus.

HTML and <abbr title="cascading stylesheets">CSS<abbr> are our tools. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus. Praesent mattis, massa quis luctus fermentum, turpis mi volutpat justo, eu volutpat enim diam eget metus.

### Blockquotes

> Lorem ipsum dolor sit amet, test link adipiscing elit. Nullam dignissim convallis est. Quisque aliquam.

## List Types

### Ordered Lists

1. Item one
   1. sub item one
   2. sub item two
   3. sub item three
2. Item two

### Unordered Lists

* Item one
* Item two
* Item three

## Tables

<div class="row">
    <div class="large-12 columns">
        <table>
  <thead>
    <tr>
      <th width="200">Table Header</th>
      <th>Table Header</th>
      <th width="150">Table Header</th>
      <th width="150">Table Header</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Content Goes Here</td>
      <td>This is longer content Donec id elit non mi porta gravida at eget metus.</td>
      <td>Content Goes Here</td>
      <td>Content Goes Here</td>
    </tr>
    <tr>
      <td>Content Goes Here</td>
      <td>This is longer Content Goes Here Donec id elit non mi porta gravida at eget metus.</td>
      <td>Content Goes Here</td>
      <td>Content Goes Here</td>
    </tr>
    <tr>
      <td>Content Goes Here</td>
      <td>This is longer Content Goes Here Donec id elit non mi porta gravida at eget metus.</td>
      <td>Content Goes Here</td>
      <td>Content Goes Here</td>
    </tr>
  </tbody>
</table>
    </div>
</div>

## Code Snippets

Syntax highlighting via Pygments

{% highlight css %}
#container {
  float: left;
  margin: 0 -240px 0 0;
  width: 100%;
}
{% endhighlight %}

## Buttons

Make any link standout more when applying the `button` class.

<a href="#" class="button">Default Button</a>
