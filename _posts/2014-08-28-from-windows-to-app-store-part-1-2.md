---
layout: post
title: "From Windows to App Store - Part 1/2"
author: dino
share: true
comments: true
excerpt:
tags:
- ios
- storreytelling
modify:
categories:
date: 2014-08-28T16:07:01+02:00
---

*Today I'm publishing a new version of my first iPhone app <a href="https://itunes.apple.com/us/app/randall/id428395953" target="_blank">RandAll</a>, almost 3 years after the original version. Here's a bit of history about how I went from being a hard core Windows user to publishing an app in the App Store.*

---


It all started late December of 2011. I had just won a great and long battle against my PC by making it dual boot Windows and Mac OS X. At that time I was mostly doing PHP stuff for my brother’s company and building my own websites for pleasure. For quite some time I had wanted to build iPhone games and apps and it was the main reason for installing Mac OS onto my PC.

My salary at that time was around 750$ a month, which sounds low but is a pretty decent salary by Croatian standards. I invested 100$ to get the iOS developer licence and forced myself to actually build something and learn Objective C. I didn’t have any friends using Macs’ at that time, let alone making iOS apps. I knew I’d be venturing into this alone with no one but Internet to help me out when I’d encounter problems… and there were problems. I was terribly wrong when I thought learning Objective C would be the only hurdle in the way.

###Getting used to working on a Mac

It was a hard switch from a Windows user to a Mac user and having to work on both operating systems every day was hell. Here are some of the major keyboard issues I had at that time:

* I was using a PC keyboard to work on a Mac, and the setup of CTRL, ALT and SHIFT buttons on PC is different than the one on a Mac. Mac has a ‘command’ button where ALT button is and the option/alt button where the Windows key is (some PC keyboards just have a hole there without buttons). There is also a function (fn) key on a Mac where PC keyboards usually have a CTRL key.

* copy&paste: Coming from Win, where I had to press CTRL + C/X/V to basically pressing ALT + C/X/V was really painful so I remapped my Mac keyboard to have the Command button all the way left where there is the function button on a Mac.

* When I used to code on a Win machine, I used HOME and END keys a lot. Mac doesn’t have those keys and instead it has a combination of command+arrow left (for home) and arrow right (for end). I must say that this made sense but switching between Win and Mac every day made me want to break something. It took some time before my brain started working well with both standards.

* Mac keyboard shortcuts are a bit weird to me even today, although I kind of like the standards like ‘command’+’,’ for app setting within most of the apps and command space to open Spotlight (or Alfred) for quick search and access to apps and files (windows made this also at some point using their Windows key. I will never understand the screenshot shortcuts on the Mac but its still better than having a separate key with just one function like it is on Windows machines :P


###Figuring out the development environment

So there I was, about to learn a programming language without even knowing what I needed and where to even start. I installed Xcode and started looking for video tutorials as I always absorb more from them than from reading books. I’m not sure if you remember those times, but it was back in the day when Xcode was one application and Interface Builder was a separate application.

![XCode and Interface Builder]({{ site.url }}/images/windows-to-app-store/XCode-and-IB.jpg)
*Interface Builder as a separate app*
{: .caption}

Interface Builder was this beautiful software that had at least 4 windows floating around your screen. I’m kind of sorry that I didn’t just ignore it at that time and built all of the UI through code.

XCode didn’t have garbage collectors so you had to worry about reserving memory for your variables and releasing the memory after you were done with them. If you mess up you get a nasty crash and some pretty funky help messages from Xcode.


![Memory Leak]({{ site.url }}/images/windows-to-app-store/memory-leak.png)
*shit Xcode says when you forget to release memory*
{: .caption}

###Learning Objective C

First batch of video tutorial I’ve watched was by <a href="https://www.youtube.com/user/thenewboston" target="_blank">thenewboston</a> on YouTube. It’s made by this pretty funny guy called Bucky. He has a very chill approach to teaching and some of his video tutorial are really funny. He has a bunch of different video tutorials so I recommend taking a look. Just watch the first 1 minute… it’s kind of funny: <a href="https://www.youtube.com/watch?v=CUcGZsJqwAo" target="_blank">Objective C Programming Tutorial - 32 - OMG, a Square Class?!</a>

I decided to study ObjC for at least 4h a day and after a week of learning I had my first app submitted to the App Store :) The app is called RandAll and it’s a tool for generating random numbers, cards and dice. In 2 years of switching app price between free and $0.99 I actually covered my apple development licence costs. .

Right after releasing the app I found out about Stanford’s open courses and there was a class “Developing iOS Apps for iPhone”. It’s absolutely the best place to start. They’ve been updating the course and following the latest versions of iOS. If you want to learn Objective C and building iOS apps, this is a great place to start: <a href="https://itunes.apple.com/us/course/developing-ios-7-apps-for/id733644550" target="_blank">Stanford: Developing iOS 7 Apps for iPhone</a>.  

In the second part of this story, I’ll write more about my experience publishing RandAll.

---

*Stay tuned by following us on [twitter](http://twitter.com/bakeryhq) or [say hi](mailto:hi@thebakery.io).*