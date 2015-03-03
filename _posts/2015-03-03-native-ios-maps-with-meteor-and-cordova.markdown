---
layout: post
title: "Native iOS Maps With Meteor and Cordova"
author: philip
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- meteorjs
- cordova
- mobile
- prototyping
image:
  feature:
date: 2015-03-03T19:38:12+08:00
---
Last week we [talked](http://thebakery.io/blog/mobile-prototyping-with-meteorjs-4-takeaways/) about using Meteor and Cordova for mobile prototyping while working on Waldo. This week we've been adding a more serious map support to the app. Below is a little video showing the map experience followed by a quick walkthrough how to get **native** maps in your Cordova Meteor apps. 

**Note:** we have not tested the new map feature on Android devices but it should be working as the plugin does support Android 

<iframe width="420" height="315" src="https://www.youtube.com/embed/C4iYRzAkqE0?rel=0&amp;vq=large" frameborder="0" allowfullscreen></iframe>

## Maps with Meteor and Cordova

David Burles has put together a great map package based on Google Maps Javascript API which can be found [here](https://github.com/dburles/meteor-google-maps). This was a logical choice for our first iteration and it worked out great. Since Waldo is a super location centric app, one would expect top notch map experience - smooth and fast. A map embedded in a WebView can only get you so far though. 

We had to look around and stumbled upon [Phonegap Google Maps plugin](https://github.com/wf9a5m75/phonegap-googlemaps-plugin). This plugin takes a different approach to map embedding and puts an actual native map control over the browser window allowing you to get native map feel with javascript API. 

## Wrapping it up for Meteor

I put together a little Meteor package (not published yet) that you can try in your own project - you can grab it from our [github](https://github.com/thebakeryio/meteor-cordova-native-map).

## Setting it up

Grab our little package and put it in your local packages folder, then add it to the project like so:

{% highlight bash %}
meteor add thebakery:mobile-map
{% endhighlight %}

Get your API key for Google Maps iOS SDK as described [here](https://github.com/wf9a5m75/phonegap-googlemaps-plugin/wiki/Tutorial-for-Mac#4b-obtain-the-google-maps-api-key-for-ios).

Help Meteor configure Cordova plugins for you by putting this in your mobile-config.js

{% highlight javascript %}
App.configurePlugin('plugin.google.maps', {
	'API_KEY_FOR_IOS': 'your-api-key'
});
{% endhighlight %}

Add the mapview to your markup like so


{% raw %}
	{{#nativeMap currentLocation=currentLocation markers=markers }}
		<!-- you can put any additional HTML overlay here -->
	{{/nativeMap}}
{% endraw %}


- currentLocation parameter should point to your current location obtained from Geolocation.latLng() - this is used to center the map
- markers is a list of markers in the following format


{% highlight javascript %}
{ _id : 'marker-id', latitude: 14.59, longitude: 121.06  }
{% endhighlight %}

Both markers and currentLocation parameters can be reactive, the map will autoupdate when changes take place.

## Build and run

Build your app and run it on iOS


{% highlight bash %}
meteor run ios-device 
{% endhighlight %}

Before launching it on your device/emulator, please make sure that the app bundle id corresponds to the value you set when obtaining Google maps SDK key.


## What's next

We'll publish the package once it's a bit more useful and mature and we confirm that it works as expected on Android. Stay tuned! If you want to help us test Waldo on iOS and Android, please send us an [email](mailto:hi@thebakery.io). 


