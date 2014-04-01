---
layout: post
title: Getting a flavour of one billion lines of code
permalink: /issue010/billion-lins-of-code
byline: Dan Abel
category: issue10
authors:
    - name: Dan Abel
      avatar: dan-abel.jpg
---

*A client wanted us to quickly tell them the state their code was in. They wanted to improve their speed of delivery. I had access to more code than I could possibly look at. I was challenged to find the art of the possible whilst trying to avoid over-focusing or worse, panicking.*

###The situation

The client were often hitting stumbling blocks shipping their software, releases were pushed back or failed to happen at all. They wanted to release more consistently. They asked Thoughtworks to examine the situation and advise them on how to release more often and well. They wanted to get to customers fast. We had 3 weeks. 

###The challenge

My role was to assess the state of the codebase to determine what was holding them back. I was asked to examine the code that made up their core platform. It was a system that collected, processed and surfaced data. And the main application that interfaced with it.

>> “A lot of languages, a lot of freedom, and a lot of code.“

The client was truly global; they had development teams everywhere. They worked at a scale I hadn’t seen before. A lot of languages, a lot of freedom, and a lot of code. More code than I could possibly look at. I was daunted by the scope and scale.

###Acknowledging the scale
 
The client had provided visibility of about 1500 repositories - around one billion lines of code. C#, C++ and Java were used widely. There was also ASP.NET, VBScript, Javascript, and C - plus a smattering of other languages. 

Hand me a codebase and a little time, and I can give you an opinion on what makes it hard to understand or even to change. Give me some time with the team who uses it and I can paint a picture of what’s working for them and the value of the patterns in use. 

But here, I couldn’t look at everything. It wasn’t going to be possible to tell an accurate and complete story. 

###Keeping it simple, keeping it broad

I decided a few flyovers or satellite imagery of *a* terrain might provide an initial context for exploration. I could see what trends were visible at a high level and use on-the-ground visits into the detail to be able to paint a fuller picture.

The first step was reaching out and making contact with the guardians of the code repositories. I needed to gather initial data. We asked each of the technology groups involved to share some codebases and to chat with us about them. We asked them what were they afraid to touch and where did they have problems? With that we started to look into what the code itself could tell us.  

With the first codebases in hand, I used some basic tools to get a feel of what I was looking at. *wc* and *grep* helped me identify file types, counts, lengths and raw Lines of Code (LOC). I also took a first pass at identifying any automated test code. 

As I saw more codebases I tuned up my techniques and added new data to my catalogue. I also sampled each codebase to get a feel for the code in detail, using the data to drive my reading. Knowing the percentage of comments in a codebase has value, but reading the code can start to tell the story of why they are there. Often describing some complexity in the code.

###Digging in

With these simple metrics I gained some insight, but it wasn’t enough. Needing options on where to go next I reached out to my team and other experts in ThoughtWorks. We picked out Source Monitor as a tool that could analyse Java, C# and C++ code - allowing us to capture metrics across many of the codebases.
 
The metrics gave me more insight into the codebases. I tried visualisations and could slice and dice into the data, highlighting interesting areas to dig into. 

###Apples and oranges

I’d looked at about 15 repositories and 10 million lines of code. I could see good and bad things about each codebase, but I needed more clarity. What was it about the data I had gathered that was important at the scale they required? Comparing the codebases didn’t seem the right thing to do. This wasn’t a contest. It was about delivering features and improvements faster. 

Setting an artificial bar didn’t seem right either. Everyone has different expectations of ‘good enough’. In the real world it’s easy to find reasons and mitigations and have the bar dismissed as chasing perfection - easily dismissible in the real world. 

I needed something that would give the data meaning; to help to drive clear thoughts and be a call to action.

###Open Source as Control Data
I thought more about comparisons. Someone on the team asked, 

*"what would everyone agree on as a measurement for a good enough codebase?"*

The answer was a revelation to me - open source projects that were popular and well used. Code that had been reviewed, developed and deployed by many teams in the real world.

>> “The question became: what can be learnt when we compare the complexity measurements of the codebases?”

Selecting four open source projects that could give me good insight, I performed the same analysis and compiled the results based on language and purpose. 

The question became: what can be learnt when we compare the complexity measurements of the codebases? Do we see potential weaknesses that need further examination or successes we can celebrate?

###Success
This allowed us to call out clearly what we could see. Our message was clearly received, even when the news wasn’t good. 

-> ⁂ <-

One of the most powerful indications was the amount of code we had. Particularly in comparison to the control codebases. We were able to highlight areas with too few tests and how that related to overly complex and coupled code. We also highlighted high levels of commenting - often replacing better patterns like version control or tests. 

We asked if these were the areas they were struggling with. And if the absence of modern Extreme Programming (XP) practises were contributing. Was it time to raise the bar and consider some codebases legacy?
