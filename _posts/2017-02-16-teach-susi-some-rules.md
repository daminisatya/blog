---
layout: post
title: Teach Susi some rules
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-016
category: Google Summer of Code
tags: [sample post]
imagefeature: cover9.jpg
comments: true
share: true
---

“I’m a young, naive being, sometimes unsure about my own statements, sometimes quirky and maybe rough, provocative in cases where the person who talks to me is provocative as well. In other cases I’m a friendly and a bit cute being”, says Susi.

She needs some help to train her personality and give the best assistance to it’s users, at the same time offers her help. So this blog post helps you on how to can get her help according to your needs.

Here is the data stub, susi_cognition_000.json, where you can teach susi all the manners. Like, produce some rules. There are few interesting things one must know before teaching her the rules.

{% highlight css %}
{
	“keys“ :[“belief“],
	“score“ :1,
	“phrases“:[ {“type“:“pattern“, “expression“:“*I feel *“} ],
	“process“:[],
	“actions“:[ {“type“:“answer“, “select“:“random“, “phrases“:[
	“Why do you feel $2$?“
	]}]
},
{% endhighlight %}

*“keys”* – These are the words list which helps a rule to get categorized. Like a particular rule can be categorized into happy when the keys are happy, joyous, festive.  The above is an example of a rule(JSON object), which has the following keys.

*“score”* – The score determines the priority of the rule. When there are multiple rules under same category, these gets prioritized based on the score. So when there are similar rules out there, the score tags play it’s required role.
*“phrases”* – This sub object has more fields namely type and expression. Type can be a pattern or a regular expression, defining the kind of expression which you are giving. Suppose the expression is a pattern like the above example *I feel * then the type will be a pattern. similarly for regular expressions.
*“process”* – Will explain about the process in the next example rule.
*“actions”* – This has fields like type , select and phrases. The type here defines the type of the answer to be given such as text(answer), pie charts and tables. (the current supported features). select tag ensures the random select of the answer and the phrases contains the list of possible answer styles.
The above example gives you the answer, on using the Susi service.

*http://loklak.org/api/susi.json?q=i feel super happy*

{% highlight css %}
{
  "session": {"identity": {
    "type": "host",
    "name": "127.0.0.1",
    "anonymous": true
  }},
  "count": 1,
  "answers": [{
    "metadata": {
      "hits": 1,
      "offset": 0,
      "count": 1
    },
    "data": [{
      "0": "i feel super happy",
      "1": "",
      "2": "super happy"
    }],
    "actions": [{
      "expression": "Why do you feel super happy?",
      "type": "answer"
    }]
  }]
}
{% endhighlight %}

The above JSON is the result of the susi result. Woah this is how susi replies back. So the answer is here.

{% highlight css %}
"actions": [{
      "expression": "Why do you feel super happy?",
      "type": "answer"
}]
{% endhighlight %}

The above answer format has a data

This is a sample example. Let’s dive into some more rules with different formats.

{% highlight css %}
{
	“keys“ :[“how“],
	“score“ :100,
	“example“:“How many mentions are on reddit about loklak“,
	“phrases“:[ {“type“:“pattern“, “expression“:“How many mentions are on reddit about *“}
	],
	“process“:[ {“type“:“console“, “expression“:“SELECT COUNT(*) AS count FROM rss WHERE url=’https://www.reddit.com/search.rss?q=$1$’;“}],
	“actions“:[ {“type“:“answer“, “select“:“random“, “phrases“:[
	“Here you go, $count$ times!“
	]}]
},
{% endhighlight %}

The above example is a score 100 rule with a high priority range than the previous example. This rule will try to answer the query related to Reddit mentions of a particular tag or a name. Here are few key differences to be noted.

“example” – The example key gives a sample query which is useful for understanding about the rule’s input.
“process” – This key is being used when you have to get the data from an external service. The above example is trying to query the tables being present using the SQL syntax. It is a console type of querying where the count is being calculated from the rss table from where the data can be retrieved from the URL. (Standard format for rss reader which is being supported by loklak: https://www.reddit.com/search.rss?q=term; 
For the above rule, susi response is this,

*http://loklak.org/api/susi.json?q=How many mentions are on reddit about loklak*

{% highlight css %}
{
  "session": {"identity": {
    "type": "host",
    "name": "127.0.0.1",
    "anonymous": true
  }},
  "count": 1,
  "answers": [{
    "data": [{"count": 5}],
    "metadata": {"count": 1},
    "actions": [{
      "expression": "Here you go, 5 times!",
      "type": "answer"
    }]
  }]
}
{% endhighlight %}

And here’s the required answer :

{% highlight css %}
"actions": [{
      "expression": "Here you go, 5 times!",
      "type": "answer"
 }]
{% endhighlight %}

So till now we have seen examples where we can retrieve text answers, Here comes an example which can return a table or a list of answers.

{% highlight css %}
{
	“keys“ :[“reddit“],
	“score“ :100,
	“example“:“What are the reddit articles about loklak“,
	“phrases“:[ {“type“:“pattern“, “expression“:“* reddit * about *“}
	],
	“process“:[ {“type“:“console“, “expression“:“SELECT title FROM rss WHERE url=’https://www.reddit.com/search.rss?q=$3$’;“}],
	“actions“:[ {“type“:“answer“, “select“:“random“, “phrases“:[
	“Here is the list of articles about $3$“
	]}, {“type“:“table“}]
},
{% endhighlight %}

For the above result you can even mention about type being table for getting the list of data. So here is the Susi’s response

*http://loklak.org/api/susi.json q=What are the reddit articles about loklak*

{% highlight css %}
{
  "session": {"identity": {
    "type": "host",
    "name": "127.0.0.1",
    "anonymous": true
  }},
  "count": 1,
  "answers": [{
    "data": [
      {"title": "programming"},
      {"title": "Datasets Archive"},
      {"title": "We collected 1.3 billion tweets with a distributed, peer-to-peer based free, open source twitter scraper that has a nice API for your self-made apps to evaluate the data: loklak.org"},
      {"title": "A look at Loklak.org and the Webclient progress"},
      {"title": "#Loklak Web client Test A Twitter search engine loklak.org"}
    ],
    "metadata": {"count": 5},
    "actions": [
      {
        "expression": "Here is the list of articles about loklak",
        "type": "answer"
      },
      {"type": "table"}
    ]
  }]
}
{% endhighlight %}

So the data object under answers gives you the list of titles tagged under loklak (PS: This is from Reddit)

Another example for getting data, using which one can form pie charts.

{% highlight css %}
{
	“keys“ :[“president“,“election“,“america“],
	“score“ :100,
	“comment“:“a statistical app which tries to predict the american presidential election“,
	“phrases“:[ {“type“:“regex“, “expression“:“Who will win the 2016 presidential election“},
	{“type“:“regex“, “expression“:“Who will (?:be|become) the next us president“}
	],
	“process“:[ {“type“:“console“, “expression“:“SELECT PERCENT(count) AS percent, hashtag AS president FROM (SELECT COUNT(*) AS count, hashtags AS hashtag FROM messages WHERE query=’election2016′ GROUP BY hashtags) WHERE hashtag IN (‘hillaryclinton’,’berniesanders’,’donaldtrump’);“}],
	“actions“:[ {“type“:“answer“, “select“:“random“, “phrases“:[
	“I believe the next president will be $president$ with a likelihood of $percent$ percent but I a not sure.“,
	“I can calculate a likelihood, here is my guess:“
	]},
	{“type“:“piechart“, “total“:100, “key“: “country“, “value“:“percent“, “unit“:“%“}]
},
{% endhighlight %}

So the above example gives you the predictions for the US elections. Here you go, Susi’s response.

*http://loklak.org/api/susi.json?q=Who will win the 2016 presidential election*

{% highlight css %}
{
  "session": {"identity": {
    "type": "host",
    "name": "10.67.93.57",
    "anonymous": true
  }},
  "count": 1,
  "answers": [{
    "metadata": {
      "hits": 21,
      "offset": 0,
      "count": 2
    },
    "data": [
      {
        "percent": 50,
        "president": "hillary2016"
      },
      {
        "percent": 50,
        "president": "trump2016"
      }
    ],
    "actions": [
      {
        "expression": "I believe the next president will be hillary2016 with a likelihood of 50.0 percent but I a not sure.",
        "type": "answer"
      },
      {
        "total": 100,
        "unit": "%",
        "type": "piechart",
        "value": "percent",
        "key": "country"
      }
    ]
  }]
}
{% endhighlight %}

Important Nomenclature for defining the variables

Suppose the expression is of the form

"* reddit * about *"

Using the above expression the following sentences can be formed. “What are the Reddit articles about Loklak” So the first set of words before reddit can be defined as $1$ variable, the set of words between reddit and about can be defined as $2$ variable and the words after about can be $3$ variable, so on. This is how the variable system works. As a whole, the complete sentence can be considered as a $0$ variable.

Some important data sources for console querying

 * http://loklak.org/api/console.json?q=SELECT%20text,%20screen_name,%20user.name%20AS%20user%20FROM%20messages%20WHERE%20query=%271%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20messages%20WHERE%20id=%27742384468560912386%27;
 * http://loklak.org/api/console.json?q=SELECT%20link,screen_name%20FROM%20messages%20WHERE%20id=%27742384468560912386%27;
 * http://loklak.org/api/console.json?q=SELECT%20COUNT(*)%20AS%20count,%20screen_name%20AS%20twitterer%20FROM%20messages%20WHERE%20query=%27loklak%27%20GROUP%20BY%20screen_name;
 * http://loklak.org/api/console.json?q=SELECT%20PERCENT(count)%20AS%20percent,%20screen_name%20FROM%20(SELECT%20COUNT(*)%20AS%20count,%20screen_name%20FROM%20messages%20WHERE%20query=%27loklak%27%20GROUP%20BY%20screen_name)%20WHERE%20screen_name%20IN%20(%27leonmakk%27,%27Daminisatya%27,%27sudheesh001%27,%27shiven_mian%27);
 * http://loklak.org/api/console.json?q=SELECT%20query,%20query_count%20AS%20count%20FROM%20queries%20WHERE%20query=%27auto%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20users%20WHERE%20screen_name=%270rb1t3r%27;
 * http://loklak.org/api/console.json?q=SELECT%20place[0]%20AS%20place,%20population,%20location[0]%20AS%20lon,%20location[1]%20AS%20lat%20FROM%20locations%20WHERE%20location=%27Berlin%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20locations%20WHERE%20location=%2753.1,13.1%27;
 * http://loklak.org/api/console.json?q=SELECT%20description%20FROM%20wikidata%20WHERE%20query=%27football%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20meetup%20WHERE%20url=%27http://www.meetup.com/?q=Women-Who-Code-Delhi%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20rss%20WHERE%20url=%27https://www.reddit.com/search.rss?q=loklak%27;
 * http://loklak.org/api/console.json?q=SELECT%20*%20FROM%20eventbrite%20WHERE%20url=%27url=https://www.eventbrite.com/e/?q=global-health-security-focus-africa-tickets-25740798421%27;