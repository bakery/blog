---
layout: post
title: "Webpack Config: Modules Directories + Define"
author: philip
share: true
comments: true
excerpt:
tags:
- webpack
- react
- redux
- modulesDirectories
- DefinePlugin
modified:
categories: 
excerpt:
image:
  feature:
date: 2016-04-14T00:15:27+01:00
---
This is a quick follow up on Raja Rao DV's [excellent article](https://medium.com/@rajaraodv/webpack-the-confusing-parts-58712f8fcad9#.h19uxlkfw) on Webpack configuration. I've discovered the following 2 bits while migrating one of our [old hackathon projects](https://github.com/thebakeryio/openmic) to React+Redux.

## Module directories

Here's a snapshot of a typical React + Redux application

![React + Redux application structure]({{ site.url }}/images/project-tree.png)

Now, let's say you are trying to render an App Container inside your app.js. This might look something like this

<script src="https://gist.github.com/callmephilip/2af75ed2fa5a75d1e8db9f3a30b1fb67.js"></script>

Notice the relative path ```'./containers/App'``` which has to be adjusted every time you import containers/components based on where you use them. Enter [module directories](https://webpack.github.io/docs/configuration.html#resolve-modulesdirectories):    

<script src="https://gist.github.com/callmephilip/089274f914bb17d5c0b6612ffabdf07c.js"></script>

This allows you to reference your modules using shorter path from anywhere in your app - when resolving modules in import statements, webpack will go over the list of provided directories. This allows us to transform app.js into

<script src="https://gist.github.com/callmephilip/1da9e3e488156e2a2c91c3a52d940ec4.js"></script>

## DefinePlugin

Say you are using Parse.com/Parse Server to sync data in your webapp and you need to initialize the SDK using application ID and API key. Define plugin will inject specified variables into your bundle and you can take advantage of environmental settings on your server:

<script src="https://gist.github.com/callmephilip/0129e0d67f906fa5b6129cec873d7e23.js"></script> 

You can now reference these values as globals in your js modules:

<script src="https://gist.github.com/callmephilip/97b8e98d49ed116461a4b986bf996312.js"></script>