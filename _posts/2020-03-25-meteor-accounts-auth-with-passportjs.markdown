---
layout: post
title: "Meteor accounts authentication with Passportjs"
author: philip
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- meteorjs
- passportjs
- authentication
- authorization
- expressjs
date: 2020-03-28T10:04:16+00:00
---

TL;DR

If you know exactly what's going on and just want to grab some code and get going, here's the [gist](https://gist.github.com/callmephilip/428f11a1bb28cace7fa8ba4b066c06de). Otherwise, read on.

## Why would I need this

In case you have a Meteor based project you have been working on for a while, chances are you came across a need to pull it apart at some point to setup a separate API server, for example, that you want to run somewhere else (e.g. a minimal express server or smth along these lines).

As part of the API refactoring, you will need to take care of the authentication layer - you want API requests authenticated against your Meteor.users collection. Below is an example of such setup using Express and Passport.js. We will be using Mongoose for data access.

## What is Passport.js

From their [website](http://www.passportjs.org/)

> Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based web application. A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.

To support authentication with our Meteor based system, we will be using Passport.js username+password strategy. Strategy (in the case of Passport.js) is a fancy word for "implementation" (which in turn is a fancy word for "getting things to work").

## Username + Password Strategy for Meteor Accounts

The first thing we need to do is map username + password to the Meteor user. Here's what this looks like on top of Passport's LocalStrategy:

<script src="https://gist.github.com/callmephilip/ed7d1548d1561f958a9dccac5124dc78.js"></script>

If authentication succeeds, we return a JSON serialized Meteor.users collection record that gets attached to each request. The next step is to tell Passport how to serialize and deserialize (which basically means "look up" in this case) the user object to use in sessions (in case you need sessions). Here's a very basic way to do this:

<script src="https://gist.github.com/callmephilip/32941ceb2fd967a4ac25e1dac69e8241.js"></script>

## Connecting the dots

Now that we told Passport how to verify authentication and serialize/deserialize user, we can connect it to the express server we are running. I am going to show you 2 scenarios below: basic auth that you can use for your API endpoints and a generic session based setup with a login form.

### Basic Auth

We are gonna add an `/api` endpoint requiring requests to contain authorization header with base64 encoded `username:password` pair. See [this](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) for more details. Here's what this looks like with Passport:

<script src="https://gist.github.com/callmephilip/406827aa0db7fa6f3ab1e9616334b3f0.js"></script>

### Sessions

Let's say we want to protect the landing page of the API server and have humans (e.g. admins) log in using their credentials. Here is a basic setup with Passport, again using our strategies from 2 minutes ago:

<script src="https://gist.github.com/callmephilip/06c870c3479b90c9b03ee5f1a43a83d1.js"></script>

## Wrap up

For a complete (although basic) boilerplate for this solution, take a look at this gist [here](https://gist.github.com/callmephilip/428f11a1bb28cace7fa8ba4b066c06de). 
