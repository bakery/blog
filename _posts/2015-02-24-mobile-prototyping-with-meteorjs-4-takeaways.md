---
layout: post
title: "Mobile prototyping with Meteorjs - 4 takeaways"
author: philip
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- meteorjs
- cordova
- mobile
- prototyping
image:
  feature:
date: 2015-02-24T16:24:48+08:00
---
As a lot of you know, Meteorjs integrates with Cordova allowing you to build cross platform mobile apps using javascript, css and html. On top of that, Meteor allows you to share parts of your codebase between client and server so one can build both mobile UI and application backend required to power the app. Below is a quick recap of our experience prototyping mobile app codenamed 'Waldo' using Meteorjs.

## Meet Waldo: quick intro

Waldo is a concept we had been playing with internally for some time until we decided to put it into a somewhat solid state people can interact with. 

Waldo lets you post geotagged content across different channels. All the content is surfaced and organized by location, as opposed to who your friends are (Facebook) or who you follow (Twitter). Unlike Foursquare, Waldo does not focus exclusively on venues - you can add any bit of text, imagery, links to Waldo as long as they are linked to a certain location and can belong to a channel or multiple channels. Here's what the app looks like

<iframe width="420" height="315" src="https://www.youtube.com/embed/95R6Dsvg-v8??rel=0&amp;vq=large&amp;controls=0" frameborder="0" allowfullscreen></iframe>


## 1 - Choosing mobile UI

We had had some experience using [Ratchet](http://goratchet.com/) for mobile UI for [Meteor Day Checkin](http://meteorday.meteor.com/). This worked  OK for an oversimplified UI but we could definitely see a lot of limitations as we wanted to push our explorations slightly further. With Waldo we opted for [Ionic](http://ionicframework.com/) which now has a very nice integration with Meteor through [Meteoric](http://meteoric.github.io/) thanks to the outstanding work by [Nick Wientge](https://twitter.com/nwientge) from [Differential](http://differential.com/).

Meteoric comes with a few demo apps ([Meteor Hunt](https://github.com/meteoric/meteorhunt), [Contacts](https://github.com/meteoric/contacts)) showcasing all the goodies in the toolkit. Cross referencing Ionic's [official documentation](http://ionicframework.com/docs/) against Meteoric's repository together with the demo apps usually gets you where you need to be.  

## 2 - Routing and views 

As most Meteorjs developers, we rely on IronRouter for both client side and server side routing. We've opted for using lightweight routes and process subscriptions on the view level as described [here](https://www.discovermeteor.com/blog/template-level-subscriptions/) combined with [this workaround](https://github.com/meteor/meteor/issues/2923#issuecomment-67577372). 

```
The good news is that view level subscrptions are coming to Meteor core. 
```

The idea is to make sure that the router renders a given  template as soon as possible without waiting for any subscriptions to be resolved and then ask for data on the view level and provide some sort of loading interface while data is being fetched from the server. As a result of this, the app has a snappy UI where things happen immediately when a person taps on tabs, buttons etc.

## 3 - Location management

Current geolocation package from MDG offers a basic way of querying device's location through a reactive variable. What ends up happening is the following: your device will try to get a rough location value and then progressively adjust the accuracy if possible. Any reactive computation or data fetching will then be invalidated and reevaluated. This can result in screen flickering + potentially expensive computations performed multiple times. There's a [PR](https://github.com/meteor/mobile-packages/pull/36) from [Scott Ananian](http://cscott.net/) to add support for [PositionOptions](https://developer.mozilla.org/en-US/docs/Web/API/PositionOptions) offering a more granular control of location querying. We ended up building a little wrapper around Geolocation.latLng() to perform basic location caching.

## 4 - Input madness

A very unexpected and bitter surprise came in the middle of the sprint with the update to [Ionic's Keyboard Cordova plugin](http://plugins.cordova.io/#/package/com.ionic.keyboard). The bug has been reported [here](https://github.com/driftyco/ionic/issues/2901). All of a sudden all our forms were severly messed up turning a functioning application into something else. Unable to locate the previous version of the keyboard plugin in question, we ended up rebuilding the forms to eliminate edge cases where the problem was occurring. In retrospect, this actually improved the feel of the app making this whole situation a blessing in disguise. Key take away - keep things simple, always.

## Conclusion

Meteorjs has enabled us to iterate extremely fast on both mobile UI and the backend part of the application. Before, a typical setup for mobile experiments would be a native iOS app with [Parse](http://parse.com/) as a backend. With isomorphic javascript minimizing context switching when working on different parts of the application architecture, Meteor is becoming our number 1 choice for mobile prototyping.       
