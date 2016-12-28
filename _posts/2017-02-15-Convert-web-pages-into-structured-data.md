---
layout: post
title: Convert webpages into structured data
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-15
category: Google Summer of Code
tags: [sample post]
imagefeature: cover10.jpg
comments: true
share: true
---

Loklak provides a new API which converts web pages into structured data in JSON. The genericscraper API helps you to scrape any web page from a given URL and provides you with the structured JSON data. Just place the URL in the given format *http://localhost:9000/api/genericscraper.json?url=http://www.google.com*

{% highlight css %}
{
  "Text in Links": [
    "Images",
    "Maps",
    "Play",
    "YouTube",
    "News",
    "Gmail",
    "Drive",
    "More Â»",
    "Web History",
    "Settings",
    "Sign in",
    "Advanced search",
    "Language tools",
    "à¤¹à¤¿à¤¨à¥à¤¦à¥€",
    "à¦¬à¦¾à¦‚à¦²à¦¾",
    "à°¤à±†à°²à±à°—à±",
    "à¤®à¤°à¤¾à¤ à¥€",
    "à®¤à®®à®¿à®´à¯",
    "àª—à«àªœàª°àª¾àª¤à«€",
    "à²•à²¨à³à²¨à²¡",
    "à´®à´²à´¯à´¾à´³à´‚",
    "à¨ªà©°à¨œà¨¾à¨¬à©€",
    "AdvertisingÂ Programs",
    "Business Solutions",
    "+Google",
    "About Google",
    "Google.com",
    "Privacy",
    "Terms"
  ],
  "Image files": [],
  "source files": [],
  "Links": [
    "http://www.google.co.in/imghp?hl=en&tab=wi",
    "http://maps.google.co.in/maps?hl=en&tab=wl",
    "https://play.google.com/?hl=en&tab=w8",
    "http://www.youtube.com/?gl=IN&tab=w1",
    "http://news.google.co.in/nwshp?hl=en&tab=wn",
    "https://mail.google.com/mail/?tab=wm",
    "https://drive.google.com/?tab=wo",
    "https://www.google.co.in/intl/en/options/",
    "http://www.google.co.in/history/optout?hl=en",
    "/preferences?hl=en",
    "https://accounts.google.com/ServiceLogin?hl=en&passive=true&continue=http://www.google.co.in/%3Fgfe_rd%3Dcr%26ei%3DR_xpV6G9M-PA8gfis7rIDA",
    "/advanced_search?hl=en-IN&authuser=0",
    "/language_tools?hl=en-IN&authuser=0",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=hi&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=bn&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=te&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=mr&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=ta&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=gu&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=kn&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=ml&source=homepage",
    "http://www.google.co.in/setprefs?sig=0_VODpnfQFFvCo-TLhn2_Kr9sRC2c%3D&hl=pa&source=homepage",
    "/intl/en/ads/",
    "http://www.google.co.in/services/",
    "https://plus.google.com/104205742743787718296",
    "/intl/en/about.html",
    "http://www.google.co.in/setprefdomain?prefdom=US&sig=__SF4cV2qKAyiHu9OKv2V_rNxesko%3D",
    "/intl/en/policies/privacy/",
    "/intl/en/policies/terms/",
    "/images/branding/product/ico/googleg_lodp.ico"
  ],
  "language": "en-IN",
  "title": "Google",
  "Script Files": []
}
{% endhighlight %}

This scrapes generic data from a given web page URL, for instance this is the current URL after scraping the main Google search page.

I wrote a generic scraper using the popular HTML scraper Java library JSoup. I scraped the generic fields like title, images, links, source files and other text between links. After the generic scraper was ready I registered the API endpoint as api/genericscraper.json along with the servlet.

![webscraper]({{ site.url }}/images/about/webscraper_1.png)

I loaded the page from the given URL and took the value from the variable url. I scraped every tag by using getElementByTag. After storing the elements, I looped through the list and retrieved the attributes from each tag. I stored the data accordingly and pushed into the JSONArray. After the necessary scraping I pushed the JSON Arrays into a JSON object and pretty printed it.

![webscraper]({{ site.url }}/images/about/webscraper_2.png)

There is an app consuming the above API called WebScraper under the Loklak apps page.

![webscraper]({{ site.url }}/images/about/webscraper_3.png)
