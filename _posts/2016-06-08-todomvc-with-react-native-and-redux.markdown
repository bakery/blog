---
layout: post
title: "TodoMVC With React Native and Redux"
author: philip
share: true
comments: true
excerpt:
tags:
- react native
- redux
- todomvc
- react native boilerplate
- baker
modified:
categories: 
excerpt:
tags: []
image:
  feature:
date: 2016-06-08T16:43:19+01:00
---
This post is a walkthrough of building a [TodoMVC](http://todomvc.com/) using React Native and Redux (without persistence for now).

<img alt="React Native TodosMVC" src="{{ site.url }}/images/todosmvc.gif">

## Quick start

<script src="https://gist.github.com/callmephilip/54da6f31f6c6148c9aaadd384c993ae8.js"></script>

**Note** There is sometimes a nasty bug with npm module installs. If you get an error related to a module not being resolved correctly, just rerun npm install so it can pick up missing modules

## Walkthrough 

Before we begin, there are few things you need to know/be comfortable with. This article assumes you already have some experience with React Native and you are also comfortable with the ideas behind [Redux](http://redux.js.org/).

We are using our home made [React Native boilerplate called Baker](https://github.com/thebakeryio/baker) boilerplate for this but you do not have to.

### Getting started

<script src="https://gist.github.com/callmephilip/7a81dbb72c5f70ba1f37f9b2361505ea.js"></script>   

This will set up a basic React Native project in TodoMVC directory - you will be prompted to enter a name of your app.    

### Take a look around 

Let's take a look at the app structure that we have so far

<img alt="Initial app Structure - TodoMVC" src="{{ site.url }}/images/todomvc-initial.png">

Most of the things in the project root directory are part of the standard React Native structure that you get after running ```react-native init```. Now if you take a closer look to the **/app** directory, you will notice there are already a few additional things in place:

**app/setup.js** is the entry point to the application, the module is used with *index.android.js* and *index.ios.js* in the project root. The module looks like this

<script src="https://gist.github.com/callmephilip/4231da9a1df44c41180f92cabaad6380.js"></script>

If you are familiar with [Redux](http://redux.js.org/), this should look fairly straighforward: we are connecting application store to the React component tree in our application

**app/reducers.js** is responsible for composing all the application reducers and making them available to the rest of the application

<script src="https://gist.github.com/callmephilip/9559094b1d447613c14c4c07f239468f.js"></script>

Notice that the Baker includes a pretty useless reducer called ```removeThisReducerOnceYouAddALegitOne``` for you to start with. We will see later how app/reducer.js module is automatically kept in sync when you are using generators to add containers to the app.  
 
<script src="https://gist.github.com/callmephilip/b9ed70ac1ebfc3334334a97653a15dbe.js"></script>

Finally, a quick look at **app/store.js**

<script src="https://gist.github.com/callmephilip/3282646603cb4ed022197c49c82cb40d.js"></script>

This is where our app's store comes to life taking advantage of the reducers we've seen in *app/reducers.js* as well as some additional middleware (and we'll see how it's useful in a second).

Let's run the app and see what it looks like at this point. Use ```npm run ios```

<img alt="TodoMVC first run" src="{{ site.url }}/images/todo-mvc-first-run.png">

At this point we have a pretty useless application up and running. Notice we also have a super useful [Remote Redux Devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en) running next to the app showing us what is going on with the application state. Remember that middleware we added to the store just a few minutes ago - that is what enabled us to have this great sneak peak into our app's inner workings.  

### Adding navigation

I wrote extensively about experimental navigation in React Native [here](http://blog.thebakery.io/react-native-experimental-navigation-with-redux/).

Once again, Baker (the boilerplate and generator system we are using) allows us to scaffold the entire navigation chunk with a single command:

<img alt="Adding navigation to React Native project" src="{{ site.url }}/images/adding-navigation.gif">

This will generate a bunch of files to plug in Tab based navigation into the. Let's reload the app in the simulator and take a look

<img alt="Basic tab navigation in the app" src="{{ site.url }}/images/basic-tabs.gif">

Head to **app/components/MainNavigation/reducer.js** and let's make tabs more relevant to our Todos application:

<script src="https://gist.github.com/callmephilip/f452dc856173c611a6153dd4828a5047.js"></script>

Our application looks like this now

<img width="270" alt="TodoMVC tabs" src="{{ site.url }}/images/todo-tabs.png">

### Creating TodoList container

Let's move on to the core of the TodoMVC application - The List. We are gonna use a container generator to create a **TodoList** container using ```npm run generate```. Start by defining **todos** reducer that will be responsible managing interactions with todos items 

<script src="https://gist.github.com/callmephilip/ea4d6b339af1bef5e52a30f667710890.js"></script>

In addition to defining the main reducer function, we are also exposing additional selectors that we can use in the component to select parts of the application state. Let's take a look at the application state:

<img alt="Application state with todos" src="{{ site.url }}/images/store-with-todos.png">

With *todos* in store, we can now focus on the TodoList container item in **app/components/TodoList/index.js**

<script src="https://gist.github.com/callmephilip/313ecfb0d92d91a13955237ecd472093.js"></script>

We are gonna take a look at **TodoItem** component in a minute. Meanwhile notice that our TodoList container is parameterized using **filter** property that can have one of the following values: *all*, *completed*, *active*. These map nicely to 3 different tabs we've defined in the application. **getSelector** function returns an appropriate selector that we have previously defined in the TodoList reducer module.

### Defining TodoItem component

To generate an empty component for the application, we are gonna use ```npm run generate``` again, choose Component option and call the new component *TodoItem*

<script src="https://gist.github.com/callmephilip/c2c33546c6b2331272954b45110ff4d8.js"></script>

TodoItem component is parameterized with a *todo* object and 2 callbacks *onToggleCompletion* and *onDelete*. These get passed down from **TodoList** container that connects it directly via Redux *dispatch*.

### Creating AddTodoItem container

One final missing part is a way to add todos in the application. We are gonna add a simple container responsible for capturing input and creating a new todo item using *addTask* action defined earlier inside TodoList actions module

<script src="https://gist.github.com/callmephilip/9eb8da23c8771093faac02a7b00967e2.js"></script>   

### Putting it all together

Let's start by updating *MainNavigation* container to render appropriate versions of TodoList containers based on the currently selected tab:

<script src="https://gist.github.com/callmephilip/517ae44a2eebab817a1881febd910c62.js"></script>

Notice how *_renderTabContent* is responsible for rendering an instance of *TodoList* container passing along a *filter* prop corresponding to the key of the current tab.

AddTodoItem is wired on the top level in the App component

<script src="https://gist.github.com/callmephilip/8794ed4dbd36cfbae71f6a98b9ab5e0e.js"></script>

Notice the usage of *Platform.OS* utility to only render *AddTodoItem* component when running on ios. There are a few minor adjustments that we had to perform (not mentioned in this article) to make sure the Android version of the app looks natural on Android - all the code for both version of the app is included in the [example repository](https://github.com/thebakeryio/todomvc-react-native)

# Conclusion

This was the first time I've built a fairly simple application using RN (React Native) and it was a lot of fun. I found the tooling to be very nice and helpful. If you understand and like React, RN feels natural. This article is not meant as a shameless plug for our in-house RN boilerplate called [Baker](https://github.com/thebakeryio/baker) but rather a showcase of how one can achieve significant improvement in productivity and happiness with a sane boilerplate+generator combo. Next time you are about to storm out to write an article about JavaScript fatigue, maybe you could write a [Yeoman based generator](http://yeoman.io/authoring/) instead and share it with others.

I'll be doing a followup post on this TodoMVC example to add a pesistence layer to the application. 

# Links

- [Source code for this example](https://github.com/thebakeryio/todomvc-react-native)
- [Yeoman based RN generator by The Bakery](https://github.com/thebakeryio/generator-rn)
- [Baker RN boilerplace by The Bakery](https://github.com/thebakeryio/baker)
- [Max Stoiber's React Boilerplate](https://github.com/mxstbr/react-boilerplate), inspiration for Baker
- [Follow us on Twitter for more goodness](https://twitter.com/bakeryhq)
