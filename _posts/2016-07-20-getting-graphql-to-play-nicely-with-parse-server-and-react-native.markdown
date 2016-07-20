---
layout: post
title: Getting GraphQL to play nicely with Parse Server and React Native
author: philip
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- graphql
- parse
- parse server
- react native
image:
  feature:
date: 2016-07-20T17:21:37+01:00
---
This is a long overdue writeup on our experience setting up GraphQL and Parse Server together for the [React Native TodoMVC project](http://blog.thebakery.io/todomvc-with-react-native-and-redux/).

## TL;DR

We've released two packages making using authenticated GraphQL queries with Parse easier: [Parse GraphQL Client](https://github.com/thebakeryio/parse-graphql-client) and [Parse GraphQL Server](https://github.com/thebakeryio/parse-graphql-server). You can see both of them in action in [TodoMVC for React Native](https://github.com/thebakeryio/todomvc-react-native).

## Setting it up

If you have been using Parse, you probably know that it uses [object level security](https://parse.com/docs/js/guide#security-object-level-access-control) based on ACL (Access Control Lists). Enforcing these constraints in queries is done by passing user's session token along. For example:

<script src="https://gist.github.com/callmephilip/7f1b6225d2f0705951f8ad15cf4e35ed.js"></script>

In order to make your GraphQL resolvers aware of these constraints, a few things need to happen.

### Getting authorization information from the client

Regardless of what GraphQL client you are using, you will have to pass authorization information (session token in our case) along with your GraphQL query/mutation. Assuming you put Parse session token inside 'Authorization' header of the request, your server code will look as follows (using [Express GraphQL](https://github.com/graphql/express-graphql)):

<script src="https://gist.github.com/callmephilip/4c73fb95543ad88ea25ca6d329fd5bf9.js"></script>

### Setting up resolvers

Once this is in place, resolvers in your schema will have access to a context variable (which in our case points to a session token):

<script src="https://gist.github.com/callmephilip/5eaece7d7183cda5d4b39fc3825c4176.js"></script>

### Rinse and repeat

Any new resolver you will be writing, will have to systematically refer to the **sessionToken** and pass it along to various methods in Parse.Query and Parse.Object (and child classes). Needless to say, this is error prone and somewhat excessive.

## Suggested solution 

[Parse GraphQL Client](https://github.com/thebakeryio/parse-graphql-client) and [Parse GraphQL Server](https://github.com/thebakeryio/parse-graphql-server) take care of passing session tokens all the way from your client to the server and configuring Parse to use them in all the queries and updates/deletes.

### Client side

Here is how you issue a GraphQL query with Parse session information attached to it in your React Native app:

<script src="https://gist.github.com/callmephilip/f74459f404fa7cb1c46a2ade67dcc279.js"></script>

### Server side

First of all, you will need to register Parse GraphQL server with your Express app instance.

<script src="https://gist.github.com/callmephilip/e84b8203e06af1da269b25634fb355bb.js"></script>

And now your resolvers will look as follows:

<script src="https://gist.github.com/callmephilip/466df8278f6082fb4af9759acefd56a0.js"></script>

Notice how resolver context already contains current user and a configured Query class based on Parse.Query. For a complete example of Todo resolver refer to [TodoMVC for React Native](https://github.com/thebakeryio/todomvc-react-native/blob/master/server/models/todo.js).

### Done!

All your queries and mutations arrive to the server with corresponding session information attached to them and all your resolvers automatically propagate it to Parse using Query class from the context.

## Credits

Parse GraphQL client is based on [Lokka GraphQL client](https://github.com/kadirahq/lokka) from folks at [Kadira](https://kadira.io/). Parse GraphQL server sits on top Lee Byron's [Express GraphQL](https://github.com/graphql/express-graphql). 
