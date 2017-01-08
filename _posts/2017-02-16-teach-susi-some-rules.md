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
