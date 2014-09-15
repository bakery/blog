---
layout: post
title: "Meteor Spotting - Building a Chrome Extension Using Meteor"
author: philip
share: true
comments: true
modified:
categories: 
tags:
- meteorjs
- chrome
- extension
- meteor spotting
image:
  feature:
date: 2014-09-15T23:44:22+02:00
---
![Meteor spotting Chrome extension]({{ site.url }}/images/meteor-spotting-chrome-extension.png)

This post documents our experience building [Meteor Spotting](http://spotting.meteor.com), a Meteor based Chrome extension to crowd source finding projects running on Meteor.

### Chrome extensions 101

Extensions are essentially web applications running within Chrome. They are built using Javascript, HTML and CSS. There are a few points that are very Chrome specicif which mostly has to do with how your extension integrates with Chrome and how different parts of it communicate between each other. You can get more details and all the relevant documentation [here](https://developer.chrome.com/extensions/devguide). 

Let's look at specific example from Meteor Spotting.

### Content scripts  

Chrome lets you inject scripts and styles into web pages. You configure this in within the content_scripts section of the manifest file for your extension (manifest.json). Here's what it looks like for Meteor Spotting:

<script src="https://gist.github.com/callmephilip/4ee68a3968460dc16c53.js"></script>

Content scripts run in a special sandbox environment. What this means is that javascript you inject cannot mess with the scripts running on the page. You can, however, access (and modify) DOM and also communicate with the background scripts. 

<script src="https://gist.github.com/callmephilip/7c132860e4193cee5ff0.js"></script>
 
We grab all script tags from the head of the page and look for the ones containig inline scripts. The content of these inline scripts is then tranferred to the background page for further investigations - specifically looking for Meteor traces. 

### Background page

Background page is the heart of your Chrome extension. Here's what it looks like in Meteor spotting

<script src="https://gist.github.com/callmephilip/24bb97f4bacc0ea639ec.js"></script>

It assembles all the scripts the extension needs. In our case background.js is where most of the magic happens. Let's take a look.

Background script is responsible for a few things, namely:
- receiving and processing 'reports' from the content script
- contacting the application server to report a spotting
- adjusting UI elements within Chrome to indicate wether a Meteor is detected using [PageAction API](https://developer.chrome.com/extensions/pageAction)

Background script is completely event driven 

<script src="https://gist.github.com/callmephilip/394f51eb647d82c75e04.js"></script>
 
### Talking to Meteor

Probably the most interesting bit for all the Meteor savyy readers is how to access Meteor application server from the extension. In other words, how does one expose an API of a Meteorjs based application? Easy-peasy, as it turns out. 

#### Say hello to DDP

The way your client javascript talks to your server javascript in Meteor is through DDP (Distributed Data Protocol) - as JSON based message protocol. Arunoda has written a great introduction about DDP which you can find [here](https://meteorhacks.com/introduction-to-ddp.html). Because DDP is an open protocol, one can write clients for it so that you can connect to your Meteorjs server application from anywhere, for example a Chrome extension. Or some [other crazy places](http://www.meteorpedia.com/read/DDP_Clients).

### DDP client

For our particular case, I grabbed [this javascript DDP client](https://github.com/mondora/ddp.js) created by folks from [Mondora](https://mondora.com)

### Micro Meteor

For Meteor Spotting, all we were interested in was the ability to talk to the Meteor based server side and remotely invoke Meteor methods. So within the extension, we've added a tiny Meteor API mimicking actual Meteor.call API method you are all familiar with

<script src="https://gist.github.com/callmephilip/72f3d1662c0c026b9738.js"></script>

With this simple setup, we can now talk to the Meteorjs application server the same way we usually do

<script src="https://gist.github.com/callmephilip/eff5c5b7b5377e55b80a.js"></script>

## Before you run away to build your own extension
     
If you are not yet spotting Meteors with all the rest, you should [jump in](http://spotting.meteor.com/). If you have any questions/comments, please do [reach out on Twitter](https://twitter.com/bakeryhq). Happy coding!      