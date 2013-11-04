---
layout: post
title: "Continuous Delivery on Windows, Part I: Blame your tools"
permalink: /issue06/cd-in-windows-part-1
subtitle: 
byline: Rachel Laycock
category: issue06
authors:
    - name: Rachel Laycock
      twitter: rachellaycock
      avatar: rachel-avatar.jpg
---
The world of development and operations tooling and practices has moved on considerably in the last 10 years, when copying a dll onto a file-share or worse, installing software with a CD was the norm. The movement of DevOps, combining the practice of dev and ops working together and automation tooling, has enabled us to release well-tested features into many production-like environments.

> "Tooling is a solved problem in DevOps... Except if you are in Windows."
		 	 	 							
I keep hearing tooling is a solved problem in DevOps. But is that really the case on Windows? Let’s look at some of the technical challenges you will face on the Windows platform. With any problem, I like to break it up into understandable pieces. For Continuous Delivery (CD) on Windows these are: Build, Deployment, and Environment Provisioning. This month I’ll focus on Build.
		 	 	 		
## Build											
This is one of the few areas that is actually a solved problem in Windows. The only real challenges are self-imposed through bad tooling choices. Build is made up of source control management (SCM) and the orchestration of compilation, testing and packaging your application for deployment. For these tasks, you should choose tools that support the practice of Continuous Integration (CI), and that enable you to manage your builds exactly how you want them. Your tool should be able to visualize at what stage your build is at and give the team immediate feedback if it is broken. 

## Source Control Management
Most teams will not necessarily choose their SCM tool in Windows. They usually have TFS as part of their Visual Studio installations and without prior knowledge will believe it solves the problem. After all, it versions your code and stores it in a central location. What more do you want? Quite a bit. When you are doing CI, everyone on the team should be checking in once a day, but not on a broken build and your SCM should support that. TFS has two major failings, which until solved will always make me choose any alternative like git. Unlike git, TFS allows server side merging, but does not allow local commits. Why is this a problem? Lets start with server side merging. 

> "I like doing CI so I don’t like using TFS."

### Server side merging
As a developer if I build and run tests locally and they pass I expect the same behaviour when I commit to the server. However, TFS allows you to push without pulling. So instead of informing you that you don’t have the same version of code that is on the server it will attempt to merge it for you. If this merge fails then the build will break. A broken build means no one else can check-in, which can slow the team down while they wait for it to be fixed.

### No local commits
One of the features I love about git is the ability to keep checking in **locally** and therefore keep a detailed log of all my changes, allowing me to revert back to a different point in time. When I am ready to commit to the server I can use rebase to commit all of my commits in order on top of the server commit stack. So the record of commits is clean and clear. This feature is not available in TFS and I miss it. Yes you have shelvesets, but they are just the same as one big commit - no going back to specific points in time to allow scratch refactorings. You could in theory create many shelvesets, but that would quickly become unmanageable. I’d rather use a tool that enables my workflow. 

## Orchestration
This is a key part of the pipeline you are building in CD. You need to be able to orchestrate, from the moment a check-in occurs, the build, test and packaging of your application. CI Servers like TeamCity and Go are perfect for orchestration as they allow you to run scripts and get visibility into the success of each of your check-ins or, at what stage it failed.

However, you might consider doing this with the built in Team Build tool. I would not recommend this. Team Build will allow you to set up a sequential set of tasks with XAML, but as soon as you want to make changes to the set-up or run certain builds in certain circumstances, any logic really, you hit upon the maintenance problems of the XML interface and it soon becomes very slow. I’ve seen builds that take 20 minutes on Team Build take only 3 on TeamCity. 

## Compilation and testing
Compilation and testing of your application was for a long time orchestrated using XML based tools like NAnt and then MSBuild, but thanks to some lessons learned from the Ruby community we now have a DSL tool in the form of PSake, which allows you to programmatically create build tasks and enjoy all the goodness DSLs provide over XML.

## Packaging
Finally you will want to package your application and for that you can use NuGet. It suffers from it’s interface, but it does allow you to package up your dll’s with their configuration into components you can then version and manage in NuGet.

> "If your tools slow you down... then choose better tools"

## Choose the right tool for the job
There really is no excuse for not getting the build part of CD right, unless you choose tools which are difficult to understand, manage or modify. I know TFS and Team Build are already paid for in many cases, but that does not make them the right tool for the job.

If your tools slow you down or hinder your ability to do CI then choose better tools. Do yourself a favour, until TFS and TeamBuild improve, choose ones that support CI.  Unlike deployment and environment provisioning in Windows, build is a solved problem so: why make a rod for your own back?
