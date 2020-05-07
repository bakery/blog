---
layout: post
title: "Debugging FastAI Image data bunches"
author: philip
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- fastai
- databunch
- images
date: 2020-05-07T12:04:16+00:00
---

Below is a little utility script that helps you visualize image data bunches you pass down to FastAI learners. It produces a chart as follows (based on FastAI pets example) 

![Image databunch from FastAI pets example]({{ site.url }}/images/fast-ai-image-databunch-debug.png)

You can plug this in directly into your notebook like so

<script src="https://gist.github.com/callmephilip/df9f09c98e12a4f09fea43eabfd18717.js"></script>
