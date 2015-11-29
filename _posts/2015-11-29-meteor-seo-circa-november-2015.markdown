---
layout: post
title: "Meteor SEO Circa November 2015"
author: philip
share: true
comments: true
excerpt:
tags:
- meteorjs
- seo
- facebook graph
- spiderable
- phantomjs
modified:
categories: 
excerpt:
image:
  feature:
date: 2015-11-29T15:26:44+00:00
---

The whole Meteor and SEO subject has been described by many as a world of pain with occasional rays of hope on the horizon. A quick google search yields these types of responses:    

[![Meteor SEO on Quora]({{site.url}}/images/howbadismeteorwithseo.png)](https://www.quora.com/How-bad-is-MeteorJS-for-an-SEO)

Manuel Schoebel [dove into the issue](http://www.manuel-schoebel.com/blog/meteor-and-seo) almost two years ago but we found that most of this stuff is a bit outdated.

I assume at this point you understand the nature of SEO problems in Meteor apps due to the dynammic nature of the applications. If you don't, you might want to start [here](https://www.quora.com/How-bad-is-MeteorJS-for-an-SEO). 

We had to set up some SEO jazz + support for Facebook's Open Graph tags (so you get nice previews of your pages on FB) and found the reality of Meteor SEO to be pretty straighforward and not so grim at all. Here's how (you can also [just jump right in](https://github.com/thebakeryio/meteor-seo-heroku)).

## Setup

For our particular case, we were dealing with the following setup:

- Iron Router for routing
- Blaze for rendering
- Deployment to Heroku using [Jordan Sissel's buildpack](https://github.com/jordansissel/heroku-buildpack-meteor)

### Step 1: Phantomjs

You will need [Phantomjs](http://phantomjs.org/) installed on your server to make sure your app can render client views server side.

For usage with Heroku, we've ended up [extending the buildpack](https://github.com/thebakeryio/heroku-buildpack-meteor/tree/feature/phantomjs) to enable Phantomjs installation and cofiguration. Adding support for phantomjs to the current buildpack [is fairly straightforward](https://github.com/jordansissel/heroku-buildpack-meteor/pull/42/files).

Note: if you use [Meteor up](https://github.com/kadirahq/meteor-up) for deployment, you get Phantomjs [by default](https://github.com/kadirahq/meteor-up/blob/master/example/mup.json#L23)

### Step 2: Spiderable

To tell Meteor that you want it to respond to requests from Google and Facebook bots in a friendly way, you will need to add spiderable module to your application

<script src="https://gist.github.com/callmephilip/65b13f4ae6fe85f635e3.js"></script>

### Step 3: Meta tags

To make sure meta tags on your pages are set accordingly, update them like so (Iron Router + Blaze in our case):

<script src="https://gist.github.com/callmephilip/dde598a163f6763d59cf.js"></script>

[DocHead](https://github.com/kadirahq/meteor-dochead) comes from the package made by good people from Kadira. It seems to be the best maintained package for manipulating document head section in Meteor.

### Step 4: Deploy and check

Once the app is deployed, you can confirm that it is being rendered correctly for the Google and Facebook bots by appending **_escaped_fragment_=** query parameter to your [url](https://meteor-heroku-seo.herokuapp.com/?_escaped_fragment_). 

If everything went OK, you should see your page rendered properly with all the html and meta tags set properly. Facebook has a [handy tool](https://developers.facebook.com/tools/debug/og/object/) allowing you to check how your links look on their site.

## Resources
- [Example App](https://github.com/thebakeryio/meteor-seo-heroku)
- [Meteor and SEO by Manuel Schoebel](http://www.manuel-schoebel.com/blog/meteor-and-seo)
- [How bad is Meteorjs for an SEO on Quora](https://www.quora.com/How-bad-is-MeteorJS-for-an-SEO)
- [Spiderable on Meteorpedia](http://www.meteorpedia.com/read/spiderable/)
- [Open Graph Object Debugger](https://developers.facebook.com/tools/debug/og/object/)