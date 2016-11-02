---
title: The Frontend Deserves its own Repository 
date: 2015-11-02 12:00:00 Z
description: Improve development speed and maintainability by splitting frontend and backend into their own repositories.-->
layout: post
header-img: img/axe-1200.jpeg
---

Even with the rise of frontend JavaScript frameworks like [Angular](https://angularjs.org/){:target="_blank"} and 
[React](https://facebook.github.io/react/){:target="_blank"}, the idea of splitting your frontend 
and backend into separate repositories is looked upon with mistrust and suspicion by many developers. Why is this? 
If you think about it, a JavaScript app is really not so different from an Android app or an iOS app. It's just a web client 
that consume a REST API. 

However, for many, the conventional wisdom is that it's easier for development and deployment 
if you keep things together. At first glance, this argument actually does make a lot of sense. It certainly is easier to worry about cloning just one repository, to only 
need to open one IDE and to have just one build process. Not only that, most developers are already accustomed to doing things this way, so 
no one has to learn a new workflow. Having said that, there are some serious benefits to breaking things up that can't be ignored.

### Improve Build Times

If you make a change to a CSS file, do you really need to re-run all of your backend API integration tests? Well, if you keep everything in one repository,
this is what ends up happening. Splitting things up means you will only build and test what has actually changed, which will result in less wasted time and resources. 
Your CI server will thank you.

### Stop Unnecessary Deployments

Rebuilds aren't the biggest problem, though, re-deployments are. A simple change to a CSS file should not require a full re-deployment of your API server. 
If you only deploy code that has actually changed, you save time and reduce the possibility for things to go wrong.  

### Reduce IDE Clutter

This doesn't necessarily have a direct effect on your end-users, but seriously, one of the immediate benefits you'll notice once you break things up is how 
much easier it is to work in your IDE. You will find be able to locate files faster and the overall performance of your IDE will be improved.  

### Microservices

One of the most popular trends in software development right now is microservices. The idea is that you should break up your monolithic application into
smaller, more manageable loosely-coupled applications with very specific responsibilities. It's very difficult to accomplish this if your frontend code is tightly coupled
with your backend code. By breaking up your frontend and backend into their own projects, you are cleanly separating responsibilities, which ultimately
makes development easier. Furthermore, splitting out your frontend into its own repository will make it much simpler to break out your backend into as many microservices as necessary. 

### Better Hosting Options

If you're able to condense your entire frontend into a collection of static files and not rely on any server-side HTML rendering (e.g. JSP), your hosting options really open up. 
For example, you can host your entire frontend on a CDN. This will make scaling much easier and cheaper because you will no longer need to worry about your servers handling requests for 
static resources or rendering HTML.     
 
### Working with Frontend Developers

In a traditional monolithic application, even frontend developers who never work on backend code will need to set up a local database, install server dependencies and run the server locally. 
But what if they're not familiar with, say, how to configure Tomcat? Or what if the developer you hired is just a freelancer and you don't want him or her to have access to your backend code? 
Maybe this is a pain point or maybe it isn't, but regardless, it's still wasted time for them to have to set up and maintain the entire application locally.
 
If you split your frontend into its own repository, you can configure it to point to a remote staging API server, rather than a local server and use a tool like 
[local-web-server](https://www.npmjs.com/package/local-web-server) to serve up the static files, just as a CDN would.  

### Conclusion

The benefits of splitting up your frontend and backend into their own repositories clearly outweigh the cons. This is especially true for large, high-traffic applications with many
contributing developers. And while this strategy may be met with some skepticism from you peers, it is quickly becoming the standard way to develop modern JavaScript-driven web applications. 
