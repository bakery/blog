---
layout: post
title: Pixels Camp Hackathon Retrospective
author: mark
share: true
comments: true
modified:
categories:
excerpt:
tags:
 - react native
 - hackathon
 - hacks
image:
 feature: pixels-camp/pixelinho.png
date: 2016-10-14T15:17:12+01:00
---

Last week, our friend Jonathan Verrecchia ([@verekia](https://twitter.com/verekia)) flew from Paris to join us in the Pixels Camp Hackathon, a 48-hour coding competition part of the broader [Pixels Camp Conference](https://pixels.camp/) in Lisbon. This was the perfect occasion for us to test out some of the tools we've been working on and lock ourselves up in a dark room for a few days.

## The Idea

As typical of engineers, we had decided on the tech stack before knowing what we'd build. We were pretty set on testing out the [Baker framework](http://baker.thebakery.io/) we've been working on, a boilerplate for kickstarting React Native apps.

While debating whether to focus on building something useful, fun or technically challenging, we decided fun would be #1, challenging #2 and useful #3. After a few beers and a meditative walk through Lisbon on Wednesday afternoon, we came up with the idea of a virtual pet that would have a positive impact on its owner and reflect his behavior. In other words, a Tamagotchi helping you pick up good habits. Pixelinho was born.

## The Hack

Although finding a table at the overpacked LX Factory venue wasn't an easy task, we managed to quickly get to work on Thursday and started hacking on Pixelinho. 

![Ready to hack]({{site.url}}/images/pixels-camp/team.JPG)
*Philip and Jonathan ready to rumble*
{: .caption}

Philip tackled the backend setup (MongoDB + GraphQL for data, Heroku for hosting, Bitrise + Testflight for Continuous Integration), Jonathan jumped on the logic (Redux + a simplified React web UI for testing out the actions) and I took a stab at the UI (logically aiming for Pixel art and discovering the subtleties of React Native UI design). 

We iterated on Pixelinho over the next 48 hours (minus a few for sleep) which eventually led to the following:

![Pixelinho]({{site.url}}/images/pixels-camp/pixelinho.png)
*Normal Pixelinho, Nerdy/Fat Pixelinho, Happy Pixelinho, and Angry/Fat Pixelinho*
{: .caption}

Pixelinho has 3 stats which evolve over time: IQ, FITNESS and FUN.

- You can level up IQ by taking him to school and answering math challenges.
- You can level up FITNESS by walking around the city.
- You can level up FUN by interracting with other Pixelinhos nearby. You can then initiate conversations which have different outcomes based on both Pixelinhos' current state.

If any of these stats is too low, Pixelinho can fall in a distressful emotional/physical state which modifies his physical appearance. 

We managed to get all the basic features we were aiming for, pretty much right in time for the demo. While we didn't win any prize for Pixelinho, we had a lot of fun building the app and learned a few lessons in the process.

## The Lessons

**Lesson 1: Pace your Testflight builds**

At around 2am on Friday evening/Saturday morning, we were hit by a minor crisis:

```
[Transporter Error Output]: ERROR ITMS-90382: "Upload limit reached.
 The upload limit for your application has been reached. Please wait 1 day and try again." 
```

This message was from Testflight after we had been agressively pushing new builds to test them out on our iPhones. 

"No worries, just plug in the cable!", you might say. Which lead to this:

![XCode issue]({{site.url}}/images/pixels-camp/xcode.png)
*a.k.a. "iOS and Xcode versions are not compatible"  
a.k.a. "Update OSX before updating Xcode"  
a.k.a. "Not something to do at 2am"*
{: .caption}

We managed to resolve the situation on the next morning but we've learned that we probably should be more conservative in pushing builds to Testflight to avoid hitting this issue again.

![Ready to hack]({{site.url}}/images/pixels-camp/5am.png)
*Fighting with Testflight at 5am*
{: .caption}

**Lesson 2: Android emulator is a pain**

We chose to only focus on the iOS version during the hackathon in order not to get sucked into compatibility issue. This turned out to be a good decision as we spent several hours post-hackathon to get the Android emulator to play nice with the Map component. We finally got it to work by running the app straight on the phone but generally speaking, the platform switch is rarely without a few hickups.

## Round Up

The React Native developement experience is incredibly productive and even more so with [the Baker](http://baker.thebakery.io/) scaffolding components, reducers and models. We'll definitely keep exploring the technology and look for ways to make the Baker even more productive. 

We'll update this post with links to the App Store and Android Store builds in the next few days.

Big thanks to the Pixels Camp crew. The event was overall very well organized (on top of being completely free). We're already looking forward to our next Portuguese Hackathon.

## Bonus track: the Sumo Fight

A short but notable interlude in our coding adventures was the Sumo fighting tournament. Philip ruthlessly defeated every opponent until the Grand Final but unsucessfully attempted a sneaky dodge move on the decisive round which lead to a nonetheless honorable 2nd place.

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZTP52uugTT4?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe>
*The Grand Final*
{: .caption}
