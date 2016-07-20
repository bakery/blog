---
layout: post
title: Introducing a Security Auditor to Meteor DevTools
author: mark
share: true
comments: true
modified:
categories: 
excerpt:
tags:
- meteorjs
- chrome devtools
- security
image:
  feature: mdt_security_collections.png
date: 2016-07-15T16:40:37+01:00
---

A few months ago, we released the [Meteor DevTools Chrome extension](https://github.com/thebakeryio/meteor-devtools), a handy tool for looking under the hood of Meteor apps. It initially came with the [DDP Monitor and Blaze Inspector plugins](http://blog.thebakery.io/introducing-meteor-devtools-for-chrome/), soon followed by the MiniMongo Explorer. The initial feedback has been great and we now have hundreds of Meteor developers using the extension daily! For those who haven't had the chance to try it yet, you can do so [over here](https://chrome.google.com/webstore/detail/meteor-devtools/ippapidnnboiophakmmhkdlchoccbgje).

We're now adding a new Security plugin to help Meteor devs follow the security best practices conviently outlined in the awesome [Meteor Guide](https://guide.meteor.com/security.html).

# Meteor Security Checklist

When getting started with Meteor, it's not very obvious what's happening behind the scenes and how the client communicates with the server. The DDP Monitor helps addressing this issue by visualizing the exchange of DDP messages. Nonetheless, many developers might not realize what the attack surface of their application is, and more importantly, that unless they take specific measures, client code will have full ready/write access to the server's database.

[The Meteor's Guide Security checklist](https://guide.meteor.com/security.html#checklist) outlines some steps every developer should consider before putting a Meteor app in production. We wanted to build a plugin helping expose potential vulnerabilities and point towards the corresponding recommendations. We started with 2 functionnalities: Packages & Collections.

# Packages

Packages installed on a Meteor application are exposed to the client via the **Package** global variable making it very easy to check whether specific packages are installed. This allows us to check that:

- **insecure** and **autopublish** packages have been removed.
- **mdg:validated-method** is used for writing secure methods.
- **aldeed:simple-schema** is used to enforce a schema on your collections.
- **audit-argument-checks** is used to verify that all methods check each of their arguments.

![Meteor Security Auditor - Packages]({{ site.url }}/images/mdt_security_packages.png)


# Collections
 
The Meteor Guide takes a strong stance against using Allow or Deny rules on Collections to use Insert/Update/Remove operations from the client. In order to expose potentially vulnerable collections, we let you test the operations on each of your collections.

![Meteor Security Auditor - Collections]({{ site.url }}/images/mdt_security_collections.png)

When clicking the Audit button, a new DDP message is generated and calls the corresponding method. 

<script src="https://gist.github.com/markdowney/b14db7cf5ab5e233d5394e29875a2627.js"></script>

If the collection is properly secured (no allow/deny rules), the server returns a DDP result message with a ```403 - Forbidden``` error. In any other case, the server will either return a success message or an error code (say if a SimpleSchema is not respected in an Insert). 

Note that we label a method as "insecure" in all cases when the result is not a ```403 error```. This means that some collections might be labeled as insecure even though the appropriate Allow/Deny rules have been setup and they present no immediate vulnerability.

As you might have noticed above, we make sure not to Insert anything in the Collections by using an empty object as an argument. Similarly, we avoid Updating or Removing existing documents by using an non-existent document Id. 

# Coming soon: Methods

The next step in our Security audit will be to test methods for invalid arguments checks. Since methods are not directly discoverable by the client, we plan to keep track of method calls while you browse around the app and save their argument type. This will allow us to call the methods again using different argument types and make sure a proper check is performed.

For issues, questions or suggestions feel free to reach out on [Github](https://github.com/thebakeryio/meteor-devtools).
