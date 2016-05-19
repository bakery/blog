---
layout: post
title: "React Native Experimental Navigation with Redux"
author: philip
share: true
comments: true
excerpt:
tags:
- react native
- redux
- navigation
modified:
categories: 
excerpt:
image:
  feature:
date: 2016-05-19T17:01:34+01:00
---
React Native is introducing a new way to manage navigation state in your application: navigation components now talk to reducers instead of storing navigation state internally. Check out [examples](https://github.com/facebook/react-native/tree/master/Examples/UIExplorer/NavigationExperimental) in the RN repository to get a feel for what it's like to use these new components.

You can grab the code for this example [here](https://github.com/thebakeryio/react-native-complex-nav)

## Battle plan

After playing with basic examples and figuring out how to hook new navigation components to a Redux store, I wanted to move on and try it with a scenario that seems to be closer to what a real app would need navigation wise.

Let's start from the end and see what the app is gonna look like

![React Native appliccation with complex navigation]({{ site.url }}/app-setup.gif)

Notice how we have a few different navigation tiers - there's a top-level card stack navigation that manages Tab views and a 'New Item' screen (top level gray screen with React logo). 

Tab navigation lives on it's own within one of the top level cards. We have 3 tabs in the app: Items, Notifications, Settings.   

The next navigational tier is within the feed tab that shows a list of items in your application. Clicking on one of the items takes you to details view screen which is still embedded with the feed tab. An example of this on twitter is you clicking on a tweet to get more details on what's going on with a tweet 

## First try

My initial attempt was to implement this in a single top level reducer. I did manage to get it to work with the scenario described above but it was not pretty

<script src="https://gist.github.com/callmephilip/8f36e30ede274638ce091749d6e9bc85.js"></script>

Not only it is super hard to reason about the behavior of this reducer, supporting and extending this looks like a nightmare. What I really need is to have separate reducers for all the different nav tiers and plug them in when needed within different parts of the application. Back to the drawing board.

## Scoped sub navigators

What if we could tackle navigation in isolation starting from the top level, adding sub navigation within our component tree when needed. After all, since navigation control is expressed using reducers, nothing stops us from connecting certain components to these reducers as we go.

### Step 1: Top level cards

The first step would be to get top level card navigation to work

![React Native card navigation]({{ site.url }}/images/top-level-nav.gif)

Let's define a reducer for this using RN's [StackReducer](https://github.com/facebook/react-native/blob/master/Libraries/NavigationExperimental/Reducer/NavigationStackReducer.js)

<script src="https://gist.github.com/callmephilip/fcbff08897c2fb5762bdf7ef73607fbc.js"></script>

We can now connect it to the navigation component using Redux connect

<script src="https://gist.github.com/callmephilip/fc9c63c59deb2bb69bc4ff5d3d809282.js"></script>

### Step 2: Tabs

![React Native tab navigation]({{ site.url }}/images/tab-nav.gif)

Our tab reducer is gonna be based on RN's [TabsReducer](https://github.com/facebook/react-native/blob/master/Libraries/NavigationExperimental/Reducer/NavigationTabsReducer.js)  

<script src="https://gist.github.com/callmephilip/07d89d9bb8b3e63645df768c5b2807e4.js"></script>

Here's how we attach this to our tab component

<script src="https://gist.github.com/callmephilip/39c594486aba0747112271f456ab7349.js"></script>

### Quick recap

Notice how we now have 2 nav hierarchies in the app coexisting in peace. Corresponding nav reducers are compact and easy to reason about. Individual reducers are combined and exposed through application Redux store 

<script src="https://gist.github.com/callmephilip/57765aff6bde6ddb0000d17254033c41.js"></script>

Here's what it looks like in the application store (don't worry about the feed part, we are gonna see it in a second)

![React Native card navigation in a tab]({{ site.url }}/images/store.png)

### Step 3: List -> Details nav

Remember how we are supposed to be able to navigate from list for details view in the feed tab? Let's implement this

![React Native card navigation in a tab]({{ site.url }}/images/list-details-nav.gif)

Let's start with defining a navigation reducer for the feed component. Once again, it is going to be a stack reducer:

<script src="https://gist.github.com/callmephilip/3b07e4b09004e5025272785c2d32dc6c.js"></script>

We can now use a NavigationCardStack component

<script src="https://gist.github.com/callmephilip/5215aec285df0ef2c61d001c45c197fa.js"></script>

### Adjusting reducer scope

An attentive reader might be able to point out the problem we are about to run into. Since our navigation reducers coexist within the app store, each of them will be trying to respond to an incoming event. With 2 stack reducers in the system (global navigation and list-details reducer), we are going to end up with 'push', 'back' and 'BackAction' actions clashing.

We could come up with special names for every new nav action but we will be loosing ability to reuse pre-made reducers. A solution I would like to suggest it so use nav keys to scope both actions and reducers as follows

<script src="https://gist.github.com/callmephilip/661842ccc4c5a8564a28539d38e3fd85.js"></script>

and a corresponding reducer now is

<script src="https://gist.github.com/callmephilip/02084695e8911f1ae553591353a277f7.js"></script>

We can now adjust reducers and components to provide this scoping. You can find the updated version of project on [Github](https://github.com/thebakeryio/react-native-complex-nav).

## Conclusion

New RN navigation approach is great for simplifying the way we reason about navigation and gets it closer to a Redux architecture which many of us are already using in React/RN apps. Setting up monolithic reducer for the app that combines multiple navigational modes has proven to be tedious and hard to maintain.

The proposed solution is to split navigation reduction into a series of scoped nav reducers where each individual reducer is respoinsible for a part of app navigation system while coordinating with other reducers using navigational key as a scope identifier.

This example is intentionally very verbose (e.g. scoping can be moved to a utility library and applied to both reducers and connector). The intetion was to make this scoping very explicit to the reader. Below is an example of scoping reducers using a helper function

<script src="https://gist.github.com/callmephilip/8eca3f1903cdd45d397b4be5ed7c07d9.js"></script>

I would be curious to hear how you manage these navigation scenarios in your apps. You can play wit this example by grabbing the code from [our github](https://github.com/thebakeryio/react-native-complex-nav)

   