---
title: Why you should separate front-end from back-end
date: 2015-11-01 12:00:00 Z
description: Improve development speed and maintainability by splitting front-end and back-end into their own repositories.-->
layout: post
published: false
---

Even with the rise of frontend JavaScript frameworks like [Angular](https://angularjs.org/){:target="_blank"} and 
[React](https://facebook.github.io/react/){:target="_blank"}, the idea of splitting your front-end 
and back-end into separate repositories is looked upon with mistrust and suspicion by many developers. For them, the conventional wisdom is
that it's easier for development and deployment if you keep things together. At first glance, this argument actually does make a lot of sense. It 
certainly is easier to worry about cloning just one repository, to only need to open one IDE and to have just one build process. Not only 
that, most developers are already accustomed to doing things this way, so no one has to learn a new workflow. Having said that, there are some 
serious benefits to breaking things up that can't be ignored.    
   
### Shorter Build Times

Assuming your front-end and back-end have some sort of build process, each build is going to take significantly longer if you're building both both frontend and backend. 
That's not the real issue, though. The real issue is that you're going to be re-building and re-testing your backend whenever you make a change to your front-end (and vice versa). 
If you fix a typo in your HTML, do you really need to re-run all of your integration tests? That's wasted time and resources. Trust me, your CI server will thank you. 

### Improved Deployments

Rebuilds aren't the biggest problem, though, re-deployments are. A simple change to a CSS file should not require a full re-deployment of your API server.  

### IDE Clutter

This doesn't necessarily have a direct effect on your end-users, but seriously, one of the immediate benefits you'll notice once you make the switch is how 
much easier it is to work in your IDE. Finding files will be faster and your overall performance of your IDE will be improved because it will have way less files to index.  

### Microservices / Serverless

One of the most popular trends in software development right now is microservices.   

### Better Hosting Options

In my opinion, you should really be striving to condense your entire frontend into a collection of static files. If you can do this, you open yourself to a whole   

### Working with Designers

Any large team is going to have certain developers and designers who work exclusively on the front-end code. In a traditional project, this means that your front-end developer is going to have 
to set up a local database, install certain dependencies and run the server locally. If you have a separate repository for the front-end, you can configure the client-side app to 
point to a remote API server and use a tool like [local-web-server](https://www.npmjs.com/package/local-web-server) to run the application. 

