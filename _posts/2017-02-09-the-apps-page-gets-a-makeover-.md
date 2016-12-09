---
layout: post
title: The apps page gets a makeover
description: "My work with Fossasia, Loklak during GSoC"
modified: 2017-02-09
category: Google Summer of Code
tags: [sample post]
imagefeature: cover6.jpg
comments: true
share: true
---

Huge transformations took place in the apps section. It’s amazing to see the count of the Loklak apps shoot up. There are more than 20 apps built using various APIs provided by Loklak. Inorder to dynamically manage the apps, apps.json was introduced.

![appsPage]({{ site.url }}/images/about/appsPage.png)

Initially there was a simple card layout. With the required name and the description of the app.

![appsPage]({{ site.url }}/images/about/appsPage_2.png)

The new tiles design has screenshots of the app and the details of the app is shown when the mouse is hovered on the screenshot. The apps are categorized based on the type of API being used. Accordingly the left navigation bar consists of all the categories.

This page is dynamic and takes the data from a new JSON object from apps API. It has all the apps and their details along with fields like categories list and the corresponding apps under it.

![appsPage]({{ site.url }}/images/about/appsPage_3.png)

The above array “categories” was used to get all the list of categories on the left navigation bar.

![appsPage]({{ site.url }}/images/about/appsPage_4.png)

The above category object is being used for getting the list of the apps under each specified category. This is being used to display the app’s details when a specific category is being clicked.

The above JSON made it easy to categorize the apps into various sections and gave a new look to the page.The tiles design was completely designed using standard CSS classes. The page is responsive and dynamic.

