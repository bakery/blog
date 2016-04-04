---
layout: post
title: "Introducing Meteor DevTools for Chrome"
author: philip
share: true
comments: true
excerpt:
tags:
- meteorjs
- chrome devtools
- meteor ddp monitor
- meteor blaze inspector
modified:
categories: 
excerpt:
image:
  feature:
date: 2016-04-04T13:06:03+01:00
---
Meteor DevTools (MD) is an extension for Chrome Developer Tools that makes the process of developing Meteor apps even more enjoyable. It also allows you to look under the hood of existing applications and learn how they are built. MD includes a plugin framework and currently comes with 2 plugins: DDP Monitor and Blaze Inspector. You can [install](https://chrome.google.com/webstore/detail/meteor-devtools/ippapidnnboiophakmmhkdlchoccbgje) it from Chrome Web Store. The extension is open source and is available on [Github](https://github.com/thebakeryio/meteor-devtools) - please chip in with your feedback. Let's take a quick look around the extension. 

# Meteor DDP Monitor

![Meteor DDP Monitor overview]({{ site.url }}/images/ddp-monitor-overview.png)

We prototyped DDP Inspector during [Global Meteor Hackathon](http://meteor-2015.devpost.com/), iterated on the intial basic version for a few weeks and came up with something pretty useful - we found ourselves using the tool on a regular basis and so we released it to the world.

Why would you need a DDP Monitor in the first place? All the Meteor framework blocks enabling communication between client and server use [DDP](https://www.meteor.com/ddp) under the hood. There's a DDP call for every subscription in your app; every time you call a method using **Method.call** API, there's a DDP message sent to the server and another message sent back to the client with the response payload, data in your collections get synced over DDP etc. In order to understand what is happening in your system, you will want to keep an eye on the DDP traces. DDP Monitor comes with a few nice features:

### Filtering messages
Message logs can get pretty crowded so it's nice to be able to focus on a specific subset of data. Looking for specific subscription? Trying to confirm what data gets passed to a method? Only interested in seeing how and if your collections get synchronized? All these scenarios and more can be simplified using filters.

![Meteor DDP Monitor filter toolbar]({{ site.url }}/images/ddp-monitor-filters.png)

### Contextual information 
The monitor is good at understanding the context of every message, here for example, we link back to the original subscription we just got a result for. This also works with various messages associated with methods. 

![Meteor DDP Monitor subscription details]({{ site.url }}/images/ddp-monitor-subscription-details.png)

### Stack trace
With stack traces, you can see where in your code the message originates from and jump right to the specific line in the file using Chrome Devtool Sources 

![Meteor DDP Monitor stack trace]({{ site.url }}/images/ddp-monitor-stack-trace.png)

### Message stats
Statistics footer gives your a bird's-eye view of the traffic in your app. How much data moves out through outbound requests? How much data comes inbound? How many subscriptions do you have? How many method calls did the app issue?

![Meteor DDP Monitor stats footer]({{ site.url }}/images/ddp-monitor-footer-stats.png)

# Blaze Inspector

![Meteor Blaze inspector]({{ site.url }}/images/meteor-blaze-inspector.png)

Blaze to DDP is what jelly is to peanut butter (if you are into PBJ sandwiches). Ever since Meteor 1.2 there are at least 3 officially supported ways to work with UI in your apps - Blaze, React and Angular. Blaze is Meteor's original view layer and despite being less in vogue compared to React/Angular, is a nice lightweight engine. 

There are tons of UIs written in Blaze out there. The problem we've seen with bigger projects is that once your codebase grows to a certain number of Blaze templates, it becomes tricky to figure out where things are - we needed a way to connect rendered HTML and the component tree. Blaze Inspector is heavily inspired by React's devtool.

## A note on the tool philosophy
There are outstanding package-based tools for Meteor out there already (yes I am looking at you [Kadira](https://kadira.io/) and [Meteor Toys](http://meteor.toys/)) that give you visibility on what's going on in your app and your app only. With Meteor DevTools we wanted to let any developer look under the hood of any Meteor application out there - you can learn about the best ways of organizing subscriptions, methods, collections and templates by looking at what real apps do.

## Before you run away
If there's a plugin you would like to see in the DevTools, [open an issue](https://github.com/thebakeryio/meteor-devtools/issues). We are on [Twitter](https://twitter.com/bakeryhq) so say hi. If you want to build something cool, we might be able to [help](http://thebakery.io/contact). 

