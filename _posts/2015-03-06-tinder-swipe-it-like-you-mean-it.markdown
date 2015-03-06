---
layout: post
title: "Tinder - Swipe it like you mean it"
author: dino
share: true
comments: true
excerpt:
tags:
- tinder
- ux
- ui
- ios
modify:
categories:
date: 2015-03-07T12:00:00+02:00
---
*First of all, I’m not a UX or UI expert, but someone once told me to speak my mind if I see someone doing something wrong or illogical. So here it goes.*

---

Tinder. Everyone knows about it and even those in relationships have checked it out to see what’s all the fuss about. I was a heavy user myself, and I have more than a few funny stories related to the usage of the app and how it worked for me in SE Asia compared to Europe, but those stories belong on my personal blog and not here.

I’ll try to describe why I think Tinder needs a redesign although it's already successful and famous for their use of swipe gestures. Not only that, they are often considered as a role model for good app design. What if I told you they did it wrong and no one even noticed? Even worse, people actually copied their mistakes.

### What is Tinder?

I’ll give you a short intro to Tinder, just in case you were living under a rock and you don’t know what Tinder is nor how it works. It is a mobile dating app that helps you find other lonely and mostly single people nearby. It also indicates if you have mutual interests or friends with other users, which helps if you are looking for something more than just… you know what ;) playing Jenga! You perv :P

![Tinder]({{ site.url }}/images/tinder.png)

After launching Tinder and connecting with your Facebook account, Tinder shows you a card/profile of a woman/man in your proximity while also displaying some basic info (name, age, mutual friend count and mutual interests count). If you want to see more pictures of that person or any more info, you have to tap the small “i” button or just tap anywhere on their card. After that, the app switches to the details screen seen in the image above. If you like the person you are viewing you either use the buttons (heart and x) or swipe their card right. Swiping left basically means that you are not interested. If that person likes you back, you get a notification and you can start chatting.

### Swipe logic... or lack of it

I think the general idea is great and simple but I believe it can be done even better. So let’s get down and dirty.

First, I would change the swipe directions. I’ve personally swiped left many times because I wanted to swipe to the next picture foolishly thinking that I’m on the details screen and just like that forever changing the course of my life and universe as we know it. Although they recently implemented “undo” feature for paid users, I still think it is a problem of bad design and now you have to pay to overcome it... brilliant! :)

I look at the digital world as an extension to the physically world we live in, and I strongly believe that pulling the profile card towards me is the natural gesture I want to make when I see someone I like since I want to pull them closer. Therefore it is only logical that if you don’t like someone, you should push their card away from you or in other words, up.

I encountered the same issue when I was doing some client work for pyr.us building a more advanced contacts app (allows you to schedule followups and write multiple notes for each of your contacts). They have a screen within the app that displays cards from your contacts in a similar way Tinder does but utilizing all four directions as separate actions. Although I believe everyone using a certain app would eventually learn which gesture is linked to which action, it is better to try and build those actions so they actually make sense. Therefore I suggested the gesture of swiping up for discarding contact's cards since it feels like you are throwing it away, while pulling it down would feel like you are taking the card and storing it.

Anyway, let’s get back to Tinder. Now that we’ve removed left and right gestures, we can finally use them for something that feels natural on mobile devices, and that is swiping through pictures of our future date. Get your creepy face on and do it like a real stalker.

### Drop that screen. Less is more

Since I don’t think Tinder needs the details screen that basically puts the app in a different mode where their reputable (but wrong) gestures just don’t work. Not only that, the UI elements that were on the bottom of the main screen move to the top right corner of the details screen. That transition right there is a UX nightmare. It only works because we got used to it. My idea was to utalize the same gesture (tapping the card itself) but instead of their transition just flip the card and extend it to fit that person's custom text and display full list of mutual friends and interests. That way we can still swipe the card up or down if we like them or not. Swiping left or right while the card is flipped would flip it back and start displaying pictures from start or end depending on the direction of that swipe. Also, after we see all the images in normal mode, swiping further right could flip the card to display the details.

Just because things work well and meet their purpose, doesn’t mean that they can’t work better while still doing the things they should. Don’t touch it! It works! Those are the famous last words of all big companies that were run over by their competitors.

If you don't agree with me that the UX is at least a bit weird, you've probably used the app too much and got indoctrinated in the process. There is no help for you and you should stick to using apps and not building them :P

That’s it. I don’t think I’m reimagining too much nor that these ideas are revolutionary or unique in any way. I’m sure someone had the same ideas... and it makes sense, because they are logical. And logic is how I roll :)

---

*Stay tuned by following us on [twitter](http://twitter.com/bakeryhq) or [say hi](mailto:hi@thebakery.io).*
