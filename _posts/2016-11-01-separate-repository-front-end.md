---
title: Why you should separate front-end from back-end
date: 2016-11-01 12:00:00 Z
description: Improve development speed and maintainability by splitting front-end and back-end into their own repositories.
published: false
header-img: 
layout: post
---

Even with the rise in recent years of frontend frameworks like [EmberJS](), [AngularJS]() and [ReactJS](), it wasn't too long 
ago that the idea of splitting your front-end and back-end into their own repositories was looked upon with mistrust and suspicion.
In fact, at a previous job, I actually suggested that we do this for a new project and was shot down because the conventional wisdom was 
that it's easier for development and deployment to keep things together. Oh, how things have changed.

That argument for keeping things in one repository actually does make sense at first glance. If you're a new developer to a project, it 
certainly seems easier to worry about cloning just one repository, to only need to open one IDE and to have just one build script. Not only 
that, but most developers are already accustomed to doing things this way, so you don't have to teach a new developer a whole new workflow. 

On the flip side, there are some major downfalls to this approach that can be remedied by breaking things up.


<!--  
Pros of single repo
- One IDE
- One thing to clone
- Easier to conceptualize (less moving parts it seems)
- Most developers are already accustomed to this workflow

Cons of single repo
- Longer build times in general, 
- changing front-end requires building and deploying back-end and vice-versa 
- too much code for your ide 
- front-end devs have to run app infrastructure locally
- doesn't work well if you go serverless

Pros of split repos
- Easier to optimize and deploy front-end code
-->  

#### Deployments



#### 